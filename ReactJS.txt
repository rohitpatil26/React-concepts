# React-concepts
Want to know basic and advanced concepts in ReactJS
React:

To create SPA web development framework. Creating indivisual component as required and merge them in single website that rendered in order that is added.

--------------------React basic------------------------

1) npm i -g create-react-app
2) create-react-app react-complete-guide --script-version 1.1.5

3) component code

class App extends Component {
  render() {
    // return (
    //   <div className="App">
    //     <h1>Hello Ract app</h1>
    //   </div>
    // );
    return React.createElement('div', {className: 'App'}, React.createElement('h1',null, 'Hello Ract app')); // similar to above commented code
  }
}

4)  create component: When creating components, you have the choice between two different ways:
	a) "presentational", "dumb" or "stateless" components
	const cmp = () => { return <div>some JSX</div> }
	
	b) "containers", "smart" or "stateful" components
	class Cmp extends Component { render () { return <div>some JSX</div> } }

5) adding dynamic expression in JSX: {<js content>}

6) sending data to child: 
	Parent:
	<Person name="max" age="28" />
	<Person> My Hobbies: racing </Person>
	Child:
	const person = (props) => {
return <p>I am {props.name} and I am {props.age} old.</p>;
}

7) Content passed in HTML element:
	Parent:
	<Person> My Hobbies: racing </Person>
	Child:
	const person = (props) => {
return (<div>
        <p>{props.children}</p>
    </div>);
}

8) Maintain component state: 
	class App extends Component {
  state = {
    persons: [
      { name: 'max', age: 28}
    ]
  };
	 render() {
    return (
      <div className="App">
	<Person name={this.state.persons[0].name} age={this.state.persons[0].age} />
	</div>
}

9) Adding event:
	<button onClick={this.<function_name_in_component>}> Call Function </button>
e.g: 
swicthHandler = () => {
    console.log('Clicked');
  }

render() {
    return (<button onClick={this.swicthHandler}>Switch Name</button>) }

10) setState: used to update state
this.state = {name: 'puran'}; 
this.setState({ person.name: 'monya'})

11) React hooks: 
import React, {useState} from 'react';

const app = prop => {
	const [usePerson, setPersonState] = useState({ person: {name: 'babu', age: 21} });
	const updateState = () => { setPersonState({person: {name: 'pora', age: 22}})};
// we can use multiple use state

	render() {
		return '<div onClick="updateState">{userPerson.person.name}</div>';
	}
}

12) Adding IF in JSX:

	a) {this.state.show ? <div>hello</div> : null}
	b) render() {
		const person = null;
		if(this.state.show) {
			person = (<div>hello</div>);
		}
		return (
			<div>{person}</div>
		);
	}

13) FOR loop template in JSX:
	render() {
		const person = null;
		if(this.state.show) {
			person = (<div>
				{this.state.persons.map(x => {
					return ( <Person name={x.name} age={x.age} />);		
				})}
				</div>);
		}
		return (
			<div>{person}</div>
		);
	}
14) adding classes:
var classss = ['red', 'bold'];
<div className={classs.join(' ')} ></div>

15) style: inline
	const style= {
		backgorundColor: 'red',
		border: '1px solid #000',
		boxShadow: '1px 1px 2px #000'
	}
	render() {
		if(true) {
			style.backgroundColor = 'green';
		}

		return (
			<div style={style}></div>
		)
	}

16) Optional for CSS packages: 
	1) Radium
	2) Styled Components
	3) CSS Module

17) Css Module: 
	To use need to run following command.
	1) npm run eject
	2) tha goto config/webpack.config.dev.js
		loader: require.resolve('css-loader'),
                options: {
                  importLoaders: 1,
                  module: true, //need to add
                  localIdentName: '[name]_[local]_[hash:base64:5]' //need to add
                },
	Also add this in prod file
	
	Now use it by
	import classes from './App.css';
	
	render() {
		<div className="classes.red"></div>
	}
	
	if want to make global 
	:global .Post { ... }


18) Life cycle hooks
	
	1) Creation life cycle: while cycle executs while creating a component:
		a) constructor(props) {
			super(props);
			this.state = {} // can initialize state here
		   }
		
		b) static getDerivedStateFromProps(props, state) {
			return state; //should not use
		}

		c) render() {
			//constructing vertual dom
		}

		d) All the child compoenet executs

		e) componentDidMount(){
			// here we can call effects such as http calls
		   }
	
	2) Update life cycle:
		a)  static getDerivedStateFromProps(props, state) {
			return state;
			// dont cause side effects
		}
		
		b) shouldComponentUpdate(nextProps, nextState) {
			// may cancel updating process
			// decide where to continue or not
			// dont cause side effects
			// should be used carefully
			return true; // will update 
			return false // will not update

			// check if update is needed than update component else not
			if(this.props.person !== nextProps.person) {
				return true;
			} else {
				return false;
			}
				
		}
		
		c) render(){
			//constructing vertual dom
			// prepare structure jsx code 
		}

		d) update child components 
		
		e) getSnapshotBeforeUpadte(prevProps, prevState) {
			// takes prevProps and prevState as input and return sanpshot were we can configure
			// not use too much
			// dont use for side effects
			// can used to save the data before the update
			return {message: 'sanpshot'}
		}

		f) componentDidUpdate(prevProps, prevState, sanpShot) {
			// a life cycle hook that tell dont with the updating 
			// can add side effect // can have api call
			// dont update state
			console.log(sanpshot) // (o/p): {message: 'sanpshot'}
		}

	3) 
	
	a) componentWillUnmount() {
		
	}
		

19) State for Functional components: 
	import React, { useEffect } from 'react';
	useEffect : this is from react 16, and helps to maintain life cycle hook like class by just this
	
	useEffect(() => {
		//this will run to every render cycle // every updates
	})
	
	a) this can be used like creation life cycle like class based component
	 
		useEffect(() => {
			//this will run to every render cycle
			// we can do side effects
		})

	// We can add multiple useEffect() in functional component
	
	b) To run useEffect only on some PROS property changed

		useEffect(() => {
			//this will run on any change in props.<selected_proerty> change
		}, [props.<property_name>])

	c) Componet rendered at first time
	
		useEffect(() => {
			//this will run only once
		}, [])

	d) on component destory
		
		useEffect(() => {
			var clearTime = setTimeout(()=>{}, 1000);
			//this will run only once
			return () => {
				// this will be called on function component destory
				clearTimeout(clearTime);
			}
		}, [])	
	e) update only when props is updated

		export default React.memo(<function_component_name>);

20) Pure component:
	shouldComponentUpdate(nextProps, nextState) {
		//validating multiple props
		if(this.props.person !== nextProps.person && this.props.changed !== nextProps.changed && this.props.show !== nextProps.show) {
				return true;
			} else {
				return false;
			}
		
	}
	class Person extend PureComponent {
		// check all properties in ShouldComponentUpdate automatically
	}

21) rendering adjaent JSX elemnts
	1) Normal with one root element
	render() {
		return (
			<div>
				<p></p>
				<span></span>
			</div>
		)
	}
		
	2) In Array
	render() {
		return [
			<p></p>,
			<span></span>
		]
			
	}

	3) creating HOC component: High order component
	Aux.js
		const aux = props => props.children;
		export default aux
	
	Main Component:
		render() {
			return (
				<Aux>
					<p></p>
					<span></span>
				</Aux>
			)
			
		}


	4) React.Fragment: gives us a conatiner to render JSX elements
	import React, { Fragment } from 'react';
	render() {
			return (
				<Fragment>
					<p></p>
					<span></span>
				</Fragment>
			)
			
		}
		

21) Higher Order components (HOC): 
	
	1) create HOC that accepts classes
		const WitClass = props => (
    			<div className={props.classes}>
        			{props.children}
    			</div>
		);

		export default WitClass;

	Main Component:
		render() {
			return (
				<WitClass classes={classes.App}>
					<p></p>
					<span></span>
				</WitClass>
			)
			
		}


	2) Second Methode with HOC:
	
		const witClass = (WrappedComponent, className) => {
    			return props => (
        			<div className={className}>
            				<WrappedComponent {...props} />
        			</div>
    			)
		}

		export default witClass;  

	Main Component:
		render() {
			return (
				<div>
					<p></p>
					<span></span>
				</div>
			)
			
		}
	
	export default withClass(App, classes.App);

22) PropTypes: Helps in setting up proper datatypes to props
	npm install --save prop-types
	
	import PropTypes from 'prop-types';
	class Person extends Component {
    render(){
        console.log('[Person] rendering...');
        return (
            <div className={[classes.Person].join(' ')}>
                <p onClick={this.props.delete}>I am {this.props.name} and I am {this.props.age} old.</p>
                <p>{this.props.children}</p>
                <input type="text" onChange={this.props.changed} value={this.props.name}/>
            </div>);
    }

}

// setting up data types
Person.propTypes = {
    delete: PropTypes.func,
    name: PropTypes.string,
    age: PropTypes.number,
    changed: PropTypes.func
} 
export default Person;

23) Ref: creating reference of element
	
	1) first method
	componentDidMount() {
		this.inputElement.focus();
	}	

	render() {
		return (
			<input key='i1' ref={(inputEl) => {this.inputElement = inputEl}}>
		);
	}
	
	2) Secons method

	constructor(props) {
		super(props);
		this.inputElementRef = React.createRef();
	}
	
	componentDidMount() {
		this.inputElement.current.focus();
	}

	render() {
		return (
			<input key='i1' ref={this.inputElementRef}>
		);
	}	
	
	3) In functional component setting element ref:
	import React, { useEffect, useRef} from 'react';
	const funCompo = props => {
			const toggleBtnRef = useRef(null);
			useeffect(()=>{
				toggleBtnRef.current.click();
			},[])
			
			return (
				<input key='i1' ref={toggleBtnRef}>
			)
			
	}

24) Context: Helps to manage communication between independent components
	a) Create Context : create new file as auth-context.js

		import React from 'react';
		const authContext = React.createContext({
    			authenticated: false,
    			login: () => {}
		});
		export default authContext;
	b) Setting value to context
		<AuthContext.Provider value={{authenticated: this.state.authenticated, login: this.loginHandler}}>
			<Cockpit/> //add all components using context
		</AuthContext.Provider>
	c) use context in child template
		<AuthContext.Consumer>
        		{context => <button onClick={context.login}>Log in</button>}
      		</AuthContext.Consumer>
	d) Using contextType in class component
		static contextType = AuthContext;
		render() {
			return {this.context.authenticated ? <p>Is Authenticated</p> : <p>Is Not Authenticated</p>}

		}
	e) Using in function component
		const authContext = useContext(AuthContext);

________________________________________________________________API Call_______________________________________________________________________________

25) Package to use api call: Axios
	https://github.com/axios/axios

26) Where to call:
	componentDidMount() {
	}

27) Sending a get request:
	import axios from 'axios';
	
	componentDidMount() {
		axios.get('https://jsonplaceholder.typicode.com/posts')
			.then(response => { 
				this.setState({
					post: response.data
				})
			})
	}

28) Transform data:
	  componentDidMount() {
		axios.get('https://jsonplaceholder.typicode.com/posts')
			.then(response => {
				const posts = response.data.slice(0, 4); // get first 4 records
				const updatePosts = posts.map(post => {...post, authr: 'papu'});
				this.setState({
					post: updatePosts
				})
			})
	}

29) avoid ifinite loop while geting record and assin it into template:

	import axios from 'axios';
	
	state= {
		loadedPost: null
	}

	componentDidUpdate() {
		if(this.props.id) {
			if(!this.state.loadedPost || (this.state.loadedPost && this.state.loadedPost.id !== this.props.id)) {
				axios.get('https://jsonplaceholder.typicode.com/posts/' + this.props.id)
				.then(response => {
					this.setState({
						loadedPost: response
					})
				})	
			}
		}
	}

30) POSTing: 
	
	import axios from 'axios';
	
	postDataHandler = () => {
		axios.post('https://jsonplaceholder.typicode.com/posts/', {
				title: '',
				content: '',
				author: 'golu' 
			})
			.then(response => {
				console.log(response);		
			});
	}

	render() {
		return (
			<button onClick={this.postDataHandler}> Save </button>
		)
	}

31) Delete: 

	import axios from 'axios';
	
	deletePostHandler = () => {
		axios.delete('https://jsonplaceholder.typicode.com/posts/' + this.props.id)
			.then(response => {
				console.log(response);		
			});
	}

	render() {
		return (
			<button onClick={this.deletePostHandler}> Delete </button>
		)
	}
	
	
32) Handling error:
		
	import axios from 'axios';
	
	deletePostHandler = () => {
		axios.delete('https://jsonplaceholder.typicode.com/posts/' + this.props.id)
			.then(response => {
				console.log(response);		
			})
			.catch(error => {
				console.log(error);
			});
	}

	render() {
		return (
			<button onClick={this.deletePostHandler}> Delete </button>
		)
	}

33) Adding Interceptor: to execute code globally

	File: index.js

	import axios from 'axios';

	axios.interceptors.request.use(request => {
		//console.log(request);
		return request;
	},
	error => { // this is used when no inter net is there
		console.log(error);
		return Promise.reject(error);	
	});

34) Interceptor: Handling respose error

	File: index.js

	import axios from 'axios';

	axios.interceptors.response.use(response => {
		//console.log(response);
		return response;
	},
	error => { // this is used when no inter net is there
		console.log(error);
		return Promise.reject(error);	
	});

35) remove interceptor:
	var myInterceptor = axios.interceptors.request.use(function () {/*...*/});
	axios.interceptors.request.eject(myInterceptor);

36) Adding common URL in the begining of url:
	 
		File: index.js

	import axios from 'axios';
	
	axios.default.baseURL = 'https://jsonplaceholder.typicode.com';
	axios.default.headers.common['Authorization'] = 'AUTH TOKEN';
	axios.default.headers.post['Content-Type'] = 'application/json';

	axios.interceptors.request.use(request => {
		//console.log(request);
		return request;
	},
	error => { // this is used when no inter net is there
		console.log(error);
		return Promise.reject(error);	
	});
	

	Usage in component:
	deletePostHandler = () => {
		axios.delete('/posts/' + this.props.id)
			.then(response => {
				console.log(response);		
			});
	}

37) Configuring interceptor:
	
	 File: axios.js
	
	import axios from 'axios';
	
	const instance = axios.create({
		baseURL: 'https://jsonplaceholder.typicode.com'
	});

	instance.default.headers.common['Authorization'] = 'AUTH TOKEN';

	export default instance;

	Usage in component:
	import instance from '../../axios';
	
	deletePostHandler = () => {
		instance.delete('/posts/' + this.props.id)
			.then(response => {
				console.log(response);		
			});
	}
	
	
___________________________________________________________________Routing_________________________________________________________________

38) npm install --save react-router react-router-dom

39) Configure Route in App.js
		
	import { BrowserRouter } from 'react-router-dom';
	
	render() {
		return (
			<BrowserRouter>
				// entire app
			</BrowserRouter>
		)
	}

40) Setting up router 
	
	import { Route } from 'react-router-dom';
	
	render() {
		return (
			<Route path="/" render={()=><h1>Home</h1>}/>
			<Route path="/home2" render={()=><h1>Home 2</h1>}/>
		)
	}

41) Route "exact" : exact path will getting loaded

42) Routing to components:
	
	import { Route } from 'react-router-dom';
	import Posts from '../../Posts/Posts';
	import NewPosts from '../../NewPosts/NewPosts';
	render() {
		return (
			<Route path="/" exact component={ Posts }/>
			<Route path="/new-posts" exact component={ Posts }/>
		)
	}
	

43) Link component: 
	
	 
	import { Route, Link } from 'react-router-dom';
	import Posts from '../../Posts/Posts';
	import NewPosts from '../../NewPosts/NewPosts';
	render() {
		return (
			<ul>
				<li> <Link to="/"> Home </Link> </li>
				<li> <Link to={{pathname: '/new-post'}}> New Post </Link> </li>
			</ul>
			
			<Route path="/" exact component={ Posts }/>
			<Route path="/new-posts" exact component={ Posts }/>
		)
	}

44) Setting up quary params and hash
	
	<li> <Link to={{pathname: '/new-post', hash: "#submit", search: "?quick-submit=true"}}> New Post </Link> </li>

45) porps in routed components: 
	
	Posts.js

	componentDidMount() {
		console.log(this.props);
	}

	we get object:

		{
			history: {
				action: 'PUSH'/'POP',
				push: ()=>{}
			},
			location: {
				hash: '',
				key: 'iiekzv',
				pathname: '/',
				search: '',
				state: undefined
			},
			match: {
				isExact: true,
				params: {},
				path: '/',
				url: '/	'	
			},
			staticContext: undefined
		}

46) Getting route deatils in routed components child component using "withRouter"

	PostDetails.js
	
	import { withRouter } from 'react-router-dom';

	const postDetails = (props) => {
		console.log(props)
	}

	export default withRouter(postDetails);

47) Creating relative path:

	<li> <Link to={{pathname: this.props.match.url + '/new-post', hash: "#submit", search: "?quick-submit=true"}}> New Post </Link> </li>

48) Adding css to active link

	
	import { Route, NavLink } from 'react-router-dom';
	
 	<li> <NavLink to="/" exact activeClassName="my-class" activeStyle={{color: #F50F66, textDecoration: undeline}}> New Post </NavLink> </li>
	
	On this link active in anchor tag css class will be add "my-class" if custome class is not provided than "active" will be added

50) Pass rout params:
	
	<Route path="/:id" exact component={ Posts }/>
	
	// route to it

	<Link to={'/' + '1'}> Post 1</Link> 
	
51) Extracting route params

	componentDidMount() {
		console.log(this.props.match.params.id);
	}

52) Switch : Load only one route component
	
	import { Route, Link, Switch } from 'react-router-dom';

	<Switch>
		<Route path="/" exact component={ Posts }/>
		<Route path="/new-posts" exact component={ NewPosts }/>
		<Route path="/:id" exact component={ PostDeatils }/>
	</Switch>

53) Routing through programatically:
	
	postClickHandler = (id) => {
		//this.props.history.push('/' + id)
		this.props.history.push({pathname: '/' + id});
	}

54) Adding child route

	 <Route path={this.props.match.url + '/:id'} exact component={ Posts }/>
		     <this is parent path>   <child>

55) Capturing change in params on same component
	
	componentDidUpdate() {
		if(this.state.loadPost.id != this.props.match.params.id) {
			// load data here	
		}	
	}
	
56) Redirect :

	import { Route, Link, Switch, Redirect } from 'react-router-dom';

	<Switch>
		<Route path="/new-posts" exact component={ NewPosts }/>
		<Route path="/posts" exact component={ Posts }/>
		<Redirect from="/" to="/posts" />
	</Switch>

57) Conditional Redirect: redirect if another page according to condition

	import { Redirect } from 'react-router-dom';
	render() {

		let redirect = null;
		if(this.state.submited) {
			redirect = <Redirect to="/posts" />
		}
		return (
			{redirect}		
		)
	}	

58) 404 not found route:

	<Route render={()=><h1> Not found </h1>} /> // put this at last

59) Lazy loading / code spliting

	import React, { Component } from 'react';

const asyncComponent = (importComponent) => {
    return class extends Component {
        state = {
            component: null
        }

        componentDidMount () {
            importComponent()
                .then(cmp => {
                    this.setState({component: cmp.default});
                });
        }
        
        render () {
            const C = this.state.component;

            return C ? <C {...this.props} /> : null;
        }
    }
}

export default asyncComponent;

Uitiliz this

	const AsyncNewPost = asyncComponent(() => {
   		 return import('./NewPost/NewPost');
	});

	<Switch>
                    {this.state.auth ? <Route path="/new-post" component={AsyncNewPost} /> : null}
	</Switch>

60) React lazy 16.6
	
	import React, { Component, Suspense } from "react"	

	const Post = React.lazy(() => import('../Posts/Posts'))

	<Route path="/post" render={ () => <Suspense fallback={<div> Loading... </div>}> <Post /> </Suspense>}


61) Deployment Note: 
	
		// set base path www.meraweb.com/my-app <--- "my-app" is react app

		<BrowserRouter basename="/my-app">
		</BrowserRouter> 
___________________________________________________________ Forms ________________________________________________________________________

62) Creating custom input component:

	import React from 'react';
	import classes from './input.css';

	const input = (props) =>{
		let inputElement = null;
		let inputClasses = [classes.InputElement];

		if(props.isValid && props.shouldValidate) {
			inputClasses = [classes.InputElement];
		} else {
			inputClasses.push(classes.Invalid)
		}
	
		switch(props.elementType) {
			case ('input'):
				inputElement = <input
							className={ inputClasses.join(' ') }
							{...props.elementConfig} 
							value={props.value}
							onChange={props.changed}
						/>
				break;
			case ('textarea'):
				inputElement = <textarea
							className={ inputClasses.join(' ') }
							{...props.elementConfig}
							value={props.value}
							onChange={props.changed}
						/>
				break;
			case ('select'): 
				inputElement = (
					<select className={ inputClasses.join(' ') } value={props.value} onChange={props.changed}>
						{
							props.elementConfig.options.map(x => { 
								return <option value={x.value} key={x.value}> {x.displayValue} </option>
							});
						}
					</select>
				);
				break;
			default:
				inputElement = <input
						className={ inputClasses.join(' ') }
						{...props.elementConfig}
						value={props.value}
						onChange={props.changed}
					       />
				break;
		}

		return (
			<div className={classes.Input}>
				<label className={classes.Label}> {props.label} </label>
				{inputElement}
			</div>
		);		
	}

	export default input;


	// using above created custom input in component
	import Input from '../UI/Input/Input';

	state = {
		orderForm: {
			name: {
				elementType: 'input',
				elementConfig: {
					type: 'text',
					placeholder: 'Your Name'
				},
				value: 'Baban',
				validations: {
					required: true,
				},
				isValid: false,
				touched: false
			},
			street: {
				elementType: 'input',
				elementConfig: {
					type: 'text',
					placeholder: 'street'
				},
				value: 'test bhava gali',
				validations: {
					required: true,
				},
				isValid: false,
				touched: false
			},
			zipcode: {
				elementType: 'input',
				elementConfig: {
					type: 'text',
					placeholder: 'zip code'
				},
				value: '410061',
				validations: {
					required: true,
				},
				isValid: false,
				touched: false	
			},
			country: {
				elementType: 'input',
				elementConfig: {
					type: 'text',
					placeholder: 'country'
				},
				value: 'Unicorn',
				validations: {
					required: true,
				},
				isValid: false,
				touched: false			
			},
			email: {
				elementType: 'input',
				elementConfig: {
					type: 'text',
					placeholder: 'Email'
				},
				value: 'baban@batali.vala',
				validations: {
					required: true,
				},
				isValid: false,
				touched: false		
			},
			deliveryMethod: {
				elementType: 'select',
				elementConfig: {
					options: [
						{value: 'fastest', displayValue: 'Fastest'},
						{value: 'cheapest', displayValue: 'Cheapest'},
					]
				},
				value: 'fatest',
				isValid: false,
				touched: false	
			}
		},
		formIsValid: false
	}
	
	inputChangeHandler = (event, inputIdentifier) =>{
		const updatedOrderForm = {...this.state.orderForm};
		const updateFormElement = {...updatedOrderForm[inputIdentifier]};
		updateFormElement.value = event.target.value;
		updateFormElement.touched = true;
		updateFormElement.isValid = this.checkValidity(event.target.value, updateFormElement.validations);
		updatedOrderForm[inputIdentifier] = updateFormElement;

		const formIsValid = true;
		for(let inputIdentifier in updatedOrderForm) {
			formIsValid = updatedOrderForm[inputIdentifier].isValid && formIsValid;
		}
		
		this.setState({orderForm: updatedOrderForm, formIsValid});
	}

	orderHandler= () => {
		const formData = {};
		for(let key in this.state.orderForm) {
			//formData = {...formData, {[key]: this.state.orderForm[key].value} };
			formData[key] = this.state.orderForm[key].value;
		}
		axios.push('url', formdata).then(x=>x).catch(err=>err);
	} 

	checkValidity(value, rule) {
		let isValid = true;
		if(rule?.required) {
			isValid = value.trim() !== '';
		}

		if(rule?.minLength) {
			isValid = value.length >= rule.minLength && isValid;
		}
		
		return isValid;
	}
	
	render() {

		const formElementsArray = [];
		for (let key in this.state.orderForm) {
			formElementsArray.push({
				id: key,
				config: this.state.orderForm[key]
			});
		}
		return (
			<form onSubmit={orderHandler}>
				formElementsArray.map(element => {
					return <Input key={element.id} 
							elementType={element.elementType}
							elementConfig={...element.config.elementConfig}
							value={element.config.value}
							changed= {(event) => this.inputChangeHandler(event, element.id)}
							isValid= { element.config.isValid }
							touched= { element.config.touched }
							shouldValidate = { element.config.validations }
						/>
				})
			
				<button disabled={this.state.fromIsValid}>Submit</button>
			</form>
		)
	}

___________________________________________________ Redux _____________________________________________________________________

Redux Node:

const redux = require('redux')
const createStore = redux.createStore;

const initialState = {
    counter: 0
}

// Reducer

const rootReducer = (state = initialState, action) => {
    switch(action.type) {
        case 'INC_COUNTER':
            return { ...state, counter: state.counter + 1};
        case 'ADD_COUNTER':
            return { ...state, counter: state.counter + action.value}; 
    }
    return state;
}

// Store

const store = createStore(rootReducer);

console.log(store.getState());

// Subscription

store.subscribe(() => {
    console.log('[Subscription]', store.getState());
});

// Dispatching Action

store.dispatch({type: 'INC_COUNTER'})
store.dispatch({type: 'ADD_COUNTER', value: 10})

console.log(store.getState());


-----------------------------------------Redux in React:------------------------------------------

