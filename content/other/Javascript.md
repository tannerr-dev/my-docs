
[[dev-notes]]

[[print pdf ]]




## Notes
- you cannot make the connectedCallback of a web component async becuase it doesn't match the function signature of the htmlelement class
    - you can make an async render() function 
- when using .innerHTML is it dangerous and might allow for XSS, use .textContent
    - does .textContent sanitize??
- data-url html attributes are accessed with .dataset.url in js
- attributeChangedCallback(prop, value), web component method
- dont forget to import the web component classes in the app.js, or import tree
- history.pushState("null",:"", "/fake-url")
    - will update the back and forward button because that cycles history statese
    - pop state is back 

- a service worker is a web worker 
	- web workers are separate threads
	- but a service worker can work as a proxy and local web server
		- service worker stores requests and responses in the cache in the browser
			- can create a separate cache section within the browswer cache
            - this is separate from the network tab cache though



## Code Snippets
```js
//show the keys of an object
Object.keys(obj)
```

```javascript
 pool = new Pool({
	host: 'localhost',
	database: 'postgres',
	user:'postgres',
	password:'mynewpassword',
	port: 5432
});
```
### express & ejs
- the route for to find public depends on the nested routing js file...
	- monies js routes need ../nav/nav.css and ../nav/nav.js instead of just nav/nav .. super fucking annoying


#### auth & session

```
npm i passport-local
npm i express-session
npm i connect-flash
```
##### express session
- requires express-session
- sessions are server side in memory / in database data that corresponds to a user, logged in or not, express-session sends a session id cookie to the browser and keeps track of cookie data for that use
- this will need to be upgraded to a real db in production
##### connect-flash
- 
##### passport
- 



### hono
- if there is an error starting deno because of a tsx error there probably is just a typo in the component

## algorithms

```Javascript
// javascript recursive factorial
function factorialize(num) {
  if(num == 1 || num == 0){
    return 1
  } else {
    return (num * factorialize(num-1))
  }
  return num;
}

factorialize(5);
```


```Javascript
// javascript bubble sort
function bubble_sort(arr){
	for(let i=0; i < arr.length;i++){
		for(let j = 0; j< arr.length - 1 - i; j++){
			if (arr[j] > arr[j+1]){
				const tmp = arr[j];
				arr[j] = arr[j+1];
				arr[j +1] = tmp;
			}	
		}
	}
}
```


```
// javascript recursive factorial
function factorialize(num) {
  if(num == 1 || num == 0){
    return 1
  } else {
    return (num * factorialize(num-1))
  }
  return num;
}

factorialize(5);
```
