## React Interview Questions

Here are the most popular questions asked at interviews of front-end developers on React.js. The topics include the basics of JavaScript and web technologies and a deep understanding of the work of React.js and related technologies (Redux, MobX, and others).

**JavaScript**:

<details>
<summary>What types of data exist in JavaScript?</summary>
<div>
  <ul>
    <li>
      <b>«number»</b> - The number type represents both integer and floating point numbers.
    </li>
    <li>
      <b>«BigInt»</b> - BigInt type was recently added to the language to represent integers of arbitrary length.
    </li>
    <li>
      <b>«string»</b> - A string in JavaScript must be surrounded by quotes.
    </li>
    <li>
      <b>«boolean»</b> - The boolean type has only two values: true and false.
    </li>
    <li>
      <b>«null»</b> - The special null value does not belong to any of the types described above. It forms a separate type of its own which contains only the null value.
    </li>
    <li>
       <b>«undefined»</b> - The special value undefined also stands apart. It makes a type of its own, just like null. The meaning of undefined is “value is not assigned”.
    </li>
    <li>
      <b>«object»</b> - The object type is special. All other types are called “primitive” because their values can contain only a single thing (be it a string or a number or whatever). In contrast, objects are used to store collections of data and more complex entities.
    </li>
    <li>
      <b>symbol</b> - The symbol type is used to create unique identifiers for objects. We have to mention it here for the sake of completeness, but also postpone the details till we know objects.
    </li>
  </ul>
  <p><i>Source: <a href ="https://javascript.info/types">javascript.info</a></i></p>
</div>
</details>

<br/>

**React**:

<details>
<summary>What component life cycle methods exist in React?</summary>
<div>
  <ul>
     <li>
       <b>render()</b> — The render() method is the only required method in a class component.
       <br>
       When called, it should examine this.props and this.state and return one of the following types: React elements, Arrays and fragments, Portals, String and numbers, Booleans or null.
       <br>
       The render() function should be pure, meaning that it does not modify component state, it returns the same result each time it’s invoked, and it does not directly interact with the browser.
     </li>
    <br/>
    <li>
      <b>constructor()</b> - The constructor for a React component is called before it is mounted. When implementing the constructor for a React.Component subclass, you should call super(props) before any other statement. Otherwise, this.props will be undefined in the constructor, which can lead to bugs.
      <br>
      Typically, in React constructors are only used for two purposes: Initializing local state by assigning an object to this.state. Binding event handler methods to an instance.
      <br>
      Constructor is the only place where you should assign this.state directly. In all other methods, you need to use this.setState() instead.
    </li>
    <br/>
    <li>
      <b>componentDidMount()</b> - is invoked immediately after a component is mounted (inserted into the tree). Initialization that requires DOM nodes should go here. If you need to load data from a remote endpoint, this is a good place to instantiate the network request.
      <br/>
      This method is a good place to set up any subscriptions. If you do that, don’t forget to unsubscribe in componentWillUnmount().
    </li>
    <br/>
    <li>
      <b>componentDidUpdate(prevProps, prevState, snapshot)</b> - is invoked immediately after updating occurs. This method is not called for the initial render.
      <br>
      Use this as an opportunity to operate on the DOM when the component has been updated. This is also a good place to do network requests as long as you compare the current props to previous props (e.g. a network request may not be necessary if the props have not changed).
    </li>
    <br/>
    <li>
      <b>componentWillUnmount()</b> - is invoked immediately before a component is unmounted and destroyed. Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that were created in componentDidMount().
    </li>
    <br/>
    <li>
      <b>shouldComponentUpdate(nextProps, nextState)</b> - is invoked before rendering when new props or state are being received. Defaults to true. This method is not called for the initial render or when forceUpdate() is used. This method only exists as a performance optimization.
    </li>
    <br/>
    <li>
      <b>static getDerivedStateFromProps(props, state)</b> - is invoked right before calling the render method, both on the initial mount and on subsequent updates. It should return an object to update the state, or null to update nothing.
      <br/>
      This method exists for rare use cases where the state depends on changes in props over time.
    </li>
    <br/>
    <li>
      <b>getSnapshotBeforeUpdate(prevProps, prevState)</b> - is invoked right before the most recently rendered output is committed to e.g. the DOM. It enables your component to capture some information from the DOM (e.g. scroll position) before it is potentially changed. Any value returned by this lifecycle will be passed as a parameter to componentDidUpdate().
    </li>
    <br/>
    <li>
      <b>static getDerivedStateFromError(error)</b> - This lifecycle is invoked after an error has been thrown by a descendant component. It receives the error that was thrown as a parameter and should return a value to update state. getDerivedStateFromError() is called during the “render” phase, so side-effects are not permitted. For those use cases, use componentDidCatch() instead.
    </li>
    <br/>
    <li>
      <b>componentDidCatch(error, info)</b> - This lifecycle is invoked after an error has been thrown by a descendant component. It receives two parameters: error - The error that was thrown, info - An object with a componentStack key containing information about which component threw the error. It should be used for things like logging errors.
    </li>
  </ul>
  <img src='https://cdn-images-1.medium.com/max/1600/1*cPwvUhZrnB1dtZnjBEfXfA.png' />
  <p><i>Источник: <a href ="https://reactjs.org/docs/react-component.html#render">reactjs.org</a></i></p>
</div>
</details>
