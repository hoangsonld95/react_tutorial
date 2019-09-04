# Table of index 

## I. JSX 
*- Why using JSX* 
*- Embedding variables, functions in JSX*
*- Specifying attributes in JSX*
*- Specifying children in JSX*
*- JSX represents Objects - How babel compiles JSX* 

## II. Rendering elements
## III. Components and props 
## IV. State and lifecycle 

------------

## I. JSX :

JSX - Javascript Syntax Extension 

- **Why using JSX** : Integrate Javascript logic with markup language HTML, CSS 

- **Embedding variables, functions in JSX** : 

```
# Don't forget the semicolon
const name = 'Leson';
const element = <h1>Hello, {name}</h1>;
# Attach element with element having id 'root' in DOM 
ReactDOM.render(
	element,
	document.getElementById('root')
);
```

-	**Specifying attributes in JSX** :

Note : JSX use camelCase naming convention 

| HTML  | JSX  |
| ------------ | ------------ |
| tabindex  | tabIndex  |
| class  | className  |


```
const element = <div tabIndex="0"></div>;
const element = <img src={user.avatarURL}></img>;
```

- **Specifying children in JSX**

```
const element = (
	<div>
		<h1>big daddy</h1>
		<h1>small daddy</h1>
	</div>
);
```

- **JSX represents Objects - How babel compiles JSX**

```
# Coding style 1 
const element= (
	<h1 className="userName">
		Virtual operating system!
	</h1>
)

# Coding style 2 
const element = React.createElement(
	'h1',
	{className: 'userName'},
	'Virtual operating system!'
)

# Those 2 above coding style is identical. Babel (javascript compiler) compiles them down to this 
const element = {
	type: 'h1',
	props: {
		className: 'userName',
		children: 'Virtual operating system!'
	}
}

```


------------

## II. Rendering elements :

- **Element is 1 part of UI** 
```
const element = <h1>Big daddy</h1>
```

- **Rendering 1 element to the DOM :** 
```
const element = <h1>Big daddy</h1>;
ReactDOM.render(
	element,
	document.getElementById('root')
);
```

- **Updating the rendered DOM :**

	- Unable to change already-created element's internal contents (attributes, children) 
	So we must create a new element and re-attach it to DOM to replace the existing one 
	- React compares newly created element with existing one, only updates the changing parts.
	That's why it's efficient. 
	
	```
	function tick() {
		const element = (
			<div>
				<h1>Current time:</h1>
				<h2>{new Date().toLocaleTimeString()}</h2>
			</div>
		);
		ReactDOM.render(element, document.getElementById('root'))
	}
	setInterval(tick(), 1000)
	```



