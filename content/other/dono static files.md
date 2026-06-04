
I'll create a Hono server for Deno that serves static files.

```typescript
import { Hono } from "https://deno.land/x/hono@v4.0.5/mod.ts";
import { serveStatic } from "https://deno.land/x/hono@v4.0.5/middleware.ts";

const app = new Hono();

// Serve static files from the 'public' directory
app.use('/static/*', serveStatic({ root: './public/' }));

// Serve index.html at the root route
app.get('/', serveStatic({ path: './public/index.html' }));

// Start the server
const port = 3000;
console.log(`Server is running on port ${port}`);

Deno.serve({ port }, app.fetch);

```

The structure remains similar, but here's how to set it up for Deno:

1. Create the same project structure:
```
your-project/
├── public/
│   ├── index.html
│   ├── styles/
│   │   └── style.css
│   └── scripts/
│       └── main.js
└── server.ts
```

2. Use the same `index.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="/static/styles/style.css">
</head>
<body>
    <h1>Hello Hono!</h1>
    <script src="/static/scripts/main.js"></script>
</body>
</html>
```

3. To run the server:
```bash
deno run --allow-net --allow-read server.ts
```

Key differences from the Node.js version:
- Uses Deno's URL imports instead of npm packages
- Uses `Deno.serve()` instead of Node's server
- Requires `--allow-net` and `--allow-read` permissions
- The static middleware comes directly from Hono instead of a separate package

Would you like me to show you how to add additional features like CORS support or custom 404 handling?



---

## TSX layout / templating question

- is there a way to link a static style sheet from the server side tsx components?? i've been trying, searching and proompting, what am i missing...

- im using server side tsx to render html and i want to link a style sheet instead of using the jsx css helper, can i just link a stylesheet like normally?

*main.tsx*
```
import { Hono } from 'hono'
import { html, raw } from 'hono/html'
import { jsx} from 'hono/jsx'
import { Layout } from './layout.tsx'
import { serveStatic } from 'hono/deno'

const app = new Hono()

app.use('/static/*', serveStatic({ root: './' }))


// app.get('/', (c) => {
//   return c.text('Hello Hono!')
// })
app.get('/', (c) => {
  return c.html(
    <Layout title='tannerr.dev'>
      <h1>Welcome to tannerr.dev</h1>
      <form action="/entry" method="POST">
        <fieldset>
          <legend>This is a web form</legend>
          <label for="name">Enter your name: </label>
          <input type="text" name="name" id="name" required autofocus/>
          <button>Submit</button>
        </fieldset>
      </form>
    </Layout>
  )
})


app.post('/entry', async (c) => {
  const body = await c.req.parseBody()
  console.log(body)
  return c.redirect('/')
  // return c.body('Thank you for coming')
})

Deno.serve(app.fetch) 
```

*layout.tsx*
```
export const Layout = (props: { children: any, title?: string }) => (
  <html>
    <head>
      <title>{props.title || 'My App'}</title>
      <link href="./public/styles.css" rel="stylesheet">
    </head>
    <body>
      <nav>
        <a href="/">Home</a>
        <a href="/users">Users</a>
      </nav>
      {props.children}
    </body>
  </html>
)

```


*error output*
```
Task start deno run --allow-net main.tsx
error: The module's source code could not be parsed: Unexpected token `html`. Expected jsx identifier at file:///home/kndr/web-dev/dono/dono/layout.tsx:8:4

    <html class={html}>
     ~~~~
```