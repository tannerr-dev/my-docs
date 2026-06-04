I'll help you build a web app that fetches weather data from Open-Meteo and displays it with Observable Plot. Here's a complete solution:

## HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather Data Visualization</title>
    <script src="https://cdn.jsdelivr.net/npm/@observablehq/plot@6"></script>
    <script src="https://cdn.jsdelivr.net/npm/d3@7"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 12px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            padding: 40px;
        }

        h1 {
            color: #333;
            margin-bottom: 10px;
            font-size: 28px;
        }

        .subtitle {
            color: #666;
            margin-bottom: 30px;
            font-size: 14px;
        }

        .controls {
            display: flex;
            gap: 20px;
            margin-bottom: 30px;
            flex-wrap: wrap;
            align-items: flex-end;
        }

        .control-group {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        label {
            font-weight: 600;
            color: #333;
            font-size: 14px;
        }

        input, select {
            padding: 10px 12px;
            border: 2px solid #e0e0e0;
            border-radius: 6px;
            font-size: 14px;
            transition: border-color 0.3s;
        }

        input:focus, select:focus {
            outline: none;
            border-color: #667eea;
        }

        button {
            padding: 10px 24px;
            background: #667eea;
            color: white;
            border: none;
            border-radius: 6px;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.3s;
            font-size: 14px;
        }

        button:hover {
            background: #5568d3;
        }

        button:active {
            transform: scale(0.98);
        }

        .loading {
            text-align: center;
            padding: 40px;
            color: #667eea;
            font-size: 16px;
        }

        .error {
            background: #fee;
            border: 2px solid #fcc;
            color: #c33;
            padding: 16px;
            border-radius: 6px;
            margin-bottom: 20px;
            font-size: 14px;
        }

        .chart-container {
            margin-bottom: 40px;
            overflow-x: auto;
        }

        .metadata {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 30px;
            padding-top: 30px;
            border-top: 2px solid #f0f0f0;
        }

        .metadata-item {
            background: #f9f9f9;
            padding: 16px;
            border-radius: 8px;
            border-left: 4px solid #667eea;
        }

        .metadata-label {
            font-size: 12px;
            color: #999;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 6px;
            font-weight: 600;
        }

        .metadata-value {
            font-size: 18px;
            color: #333;
            font-weight: 600;
        }

        .metadata-unit {
            font-size: 12px;
            color: #999;
            margin-left: 4px;
        }

        @media (max-width: 768px) {
            .container {
                padding: 20px;
            }

            h1 {
                font-size: 22px;
            }

            .controls {
                flex-direction: column;
            }

            .control-group {
                width: 100%;
            }

            input, select, button {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🌤️ Weather Data Visualization</h1>
        <p class="subtitle">Real-time weather data from Open-Meteo API</p>

        <div class="controls">
            <div class="control-group">
                <label for="latitude">Latitude</label>
                <input type="number" id="latitude" placeholder="e.g., 40.7128" value="40.7128" step="0.01">
            </div>
            <div class="control-group">
                <label for="longitude">Longitude</label>
                <input type="number" id="longitude" placeholder="e.g., -74.0060" value="-74.0060" step="0.01">
            </div>
            <div class="control-group">
                <label for="variable">Variable</label>
                <select id="variable">
                    <option value="temperature_2m">Temperature (2m)</option>
                    <option value="relative_humidity_2m">Humidity</option>
                    <option value="precipitation">Precipitation</option>
                    <option value="wind_speed_10m">Wind Speed</option>
                </select>
            </div>
            <button onclick="fetchWeatherData()">Fetch Data</button>
        </div>

        <div id="error" class="error" style="display: none;"></div>
        <div id="loading" class="loading" style="display: none;">Loading data...</div>
        <div id="chart" class="chart-container"></div>
        <div id="metadata" class="metadata"></div>
    </div>

    <script src="app.js"></script>
</body>
</html>
```

## JavaScript (app.js)

```javascript
// Configuration
const API_BASE = 'https://archive-api.open-meteo.com/v1/archive';
const FORECAST_API = 'https://api.open-meteo.com/v1/forecast';

// Variable configuration
const VARIABLES = {
    temperature_2m: { name: 'Temperature', unit: '°C', color: '#ff6b6b' },
    relative_humidity_2m: { name: 'Humidity', unit: '%', color: '#4ecdc4' },
    precipitation: { name: 'Precipitation', unit: 'mm', color: '#45b7d1' },
    wind_speed_10m: { name: 'Wind Speed', unit: 'm/s', color: '#96ceb4' }
};

// Fetch weather data from Open-Meteo
async function fetchWeatherData() {
    const latitude = document.getElementById('latitude').value;
    const longitude = document.getElementById('longitude').value;
    const variable = document.getElementById('variable').value;
    const errorDiv = document.getElementById('error');
    const loadingDiv = document.getElementById('loading');
    const chartDiv = document.getElementById('chart');
    const metadataDiv = document.getElementById('metadata');

    // Validate inputs
    if (!latitude || !longitude) {
        errorDiv.textContent = 'Please enter valid latitude and longitude';
        errorDiv.style.display = 'block';
        return;
    }

    errorDiv.style.display = 'none';
    loadingDiv.style.display = 'block';
    chartDiv.innerHTML = '';
    metadataDiv.innerHTML = '';

    try {
        // Fetch 7-day forecast data
        const now = new Date();
        const endDate = new Date(now.getTime() + 7 * 24 * 60 * 60 * 1000);
        
        const params = new URLSearchParams({
            latitude: latitude,
            longitude: longitude,
            hourly: variable,
            timezone: 'auto'
        });

        const response = await fetch(`${FORECAST_API}?${params}`);
        
        if (!response.ok) {
            throw new Error(`API error: ${response.status}`);
        }

        const data = await response.json();
        loadingDiv.style.display = 'none';

        // Process and display data
        displayChart(data, variable);
        displayMetadata(data, variable);

    } catch (error) {
        loadingDiv.style.display = 'none';
        errorDiv.textContent = `Error: ${error.message}`;
        errorDiv.style.display = 'block';
        console.error(error);
    }
}

// Display chart using Observable Plot
function displayChart(data, variable) {
    const chartDiv = document.getElementById('chart');
    const hourly = data.hourly;
    const times = hourly.time;
    const values = hourly[variable];

    // Transform data for plotting
    const chartData = times.map((time, index) => ({
        time: new Date(time),
        value: values[index],
        hour: new Date(time).toLocaleString('en-US', { 
            month: 'short', 
            day: 'numeric', 
            hour: '2-digit',
            minute: '2-digit'
        })
    }));

    const variableConfig = VARIABLES[variable];

    // Create Observable Plot
    const plot = Plot.plot({
        title: `${variableConfig.name} - 7 Day Forecast`,
        width: chartDiv.offsetWidth,
        height: 400,
        margin: { left: 60, right: 20, top: 40, bottom: 50 },
        x: {
            type: 'time',
            label: 'Time'
        },
        y: {
            label: `${variableConfig.name} (${variableConfig.unit})`
        },
        marks: [
            Plot.line(chartData, {
                x: 'time',
                y: 'value',
                stroke: variableConfig.color,
                strokeWidth: 2
            }),
            Plot.dot(chartData, {
                x: 'time',
                y: 'value',
                fill: variableConfig.color,
                r: 3,
                opacity: 0.6
            })
        ],
        style: {
            fontSize: '12px',
            fontFamily: 'system-ui'
        }
    });

    chartDiv.appendChild(plot);
}

// Display metadata
function displayMetadata(data, variable) {
    const metadataDiv = document.getElementById('metadata');
    const hourly = data.hourly;
    const values = hourly[variable];

    // Calculate statistics
    const min = Math.min(...values);
    const max = Math.max(...values);
    const avg = (values.reduce((a, b) => a + b, 0) / values.length).toFixed(2);
    const variableConfig = VARIABLES[variable];

    // Get location info
    const location = `${data.latitude.toFixed(2)}°, ${data.longitude.toFixed(2)}°`;
    const timezone = data.timezone;
    const lastUpdate = new Date().toLocaleString();

    const metadata = [
        { label: 'Location', value: location },
        { label: 'Timezone', value: timezone },
        { label: 'Minimum', value: min.toFixed(2), unit: variableConfig.unit },
        { label: 'Maximum', value: max.toFixed(2), unit: variableConfig.unit },
        { label: 'Average', value: avg, unit: variableConfig.unit },
        { label: 'Last Updated', value: lastUpdate }
    ];

    metadataDiv.innerHTML = metadata.map(item => `
        <div class="metadata-item">
            <div class="metadata-label">${item.label}</div>
            <div class="metadata-value">
                ${item.value}
                ${item.unit ? `<span class="metadata-unit">${item.unit}</span>` : ''}
            </div>
        </div>
    `).join('');
}

// Fetch data on page load with default values
window.addEventListener('load', () => {
    fetchWeatherData();
});
```

## Key Features

**API Integration**: Uses **Open-Meteo's free weather API** with no authentication required

**Observable Plot**: Creates **interactive line charts** with dots marking data points

**Metadata Display**: Shows **min, max, average values**, location, timezone, and last update time

**Responsive Design**: Works well on **desktop and mobile devices**

**Error Handling**: Includes **validation and error messages**

**Variable Selection**: Choose between **temperature, humidity, precipitation, and wind speed**

## How to Use

1. **Save the HTML** as `index.html` and the JavaScript as `app.js` in the same folder
2. **Open `index.html`** in your browser
3. **Modify latitude/longitude** to any location (defaults to New York City)
4. **Select a variable** from the dropdown
5. **Click "Fetch Data"** to load and display the chart

The app fetches a **7-day hourly forecast** and displays it with statistics. You can customize the styling, add more variables, or extend it with additional features like date range selection or multiple location comparisons.
