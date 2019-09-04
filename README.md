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


------------

## III. Components & Props : 

- **Function & Class Components :**

	Components : independent, reusable pieces, accept props (arguments), return React elements.
	Class and function are possibly use interchangeably.
	The function or class name could be different with className. What matters is the className.
	If possible, try to make them to be same.
	
	```
	# Function. Props : properties argument
	function Welcome(props) {
		return (
			<h1>
				Welcome, {props.name}
			</h1>
		)
	}

	# Class. Props : properties argument
	class Welcome extends React.Component {
		render() {
			return(
				<h1>
					Welcome, {props.name}
				</h1>
			)
		}
	}
	```
	
	(?) Why is function's argument and class's argument named props 
	
	Because Babels compiles down JSX to this : 
	
	```
	# JSX
	const element = (
		<h1 className="greeting">
			Welcome guest!
		</h1>
	);
	# Babels compiles JSX to this
	const element = {
		type: 'h1',
		props: {
			className: 'greeting',
			children: 'Welcome guest!'
		}
	}
	```
	
- Rendering a component + Composing many components :  
	
	```
	# Rendering Welcome component
	function Welcome(props) {
		return (
			<h1>Welcome, {props.name}</h1>
		)
	}

	const element = <Welcome name="leson" />;

	ReactDOM.render(
		element, 
		document.getElementById('root')
	);

	# Combine many components 

	function NameInfo(props) {
		return (
			<h1>
				Welcome, {props.name}
			</h1>
		)
	}

	function EmailInfo(props) {
		return(
			<h1>
				Email: {props.email}
			</h1>
		)
	}

	function AddressInfo(props) {
		return(
			<h1>
				Address: {props.address}
			</h1>
		)
	}

	function ContactInfo(props) {
		return(
			<div>
				<h1> Contact Info : </h1>
				<NameInfo name={props.name} />
				<EmailInfo name={props.name} />
				<AddressInfo name={props.name} />
			</div>
		)
	}

	const element = <ContactInfo name="leson" email="leson@gmail.com" address="ootaku">;

	ReactDOM.render(
		element,
		document.getElementById('root')
	);

	```
	
- **Extracting components :** 

	```
	function Avatar(props) {
	  return (
		<img className="Avatar" 
			 src = {props.img_url}
		  />
	  );
	}

	function UserName(props) {
	  return(
		<div className="UserName">
		  {props.usr_name}
		</div>
	  );
	}

	function CommentText(props) {
	  return(
		<div className="CommentText">
		  {props.cmt_text}
		</div>
	  );
	}

	function CommentDate(props) {
	  return(
		<div className="CommentDate">
		  {props.cmt_date}
		</div>
	  );
	}

	function Comment(props) {
	  return (
		<div className="Comment">
		  <Avatar img_url={props.img_url} />
		  <UserName usr_name={props.usr_name} />
		  <CommentText cmt_text={props.cmt_text} />
		  <CommentDate cmt_date={props.cmt_date} />
		</div>
	  );
	}
	
	# Conventional Javascript Syntax, no big deal 
	const comment_info = {
	  img_url: 'https://placekitten.com/g/64/64',
	  usr_name: 'hoangsonld',
	  cmt_text: 'the backbones',
	  cmt_date: new Date().toLocaleDateString(),
	};      

	ReactDOM.render(
		 <Comment 
			img_url= {comment_info.img_url} 
			usr_name = {comment_info.usr_name}
			cmt_text = {comment_info.cmt_text}
			cmt_date = {comment_info.cmt_date}
		/>,
		document.getElementById('root')
	);
	```
	
- **Props are read-only** 

> 	You must not change the props. 

