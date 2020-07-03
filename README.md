## React Interview Questions

Here are the most popular questions asked at interviews of front-end developers on React.js. The topics include the basics of JavaScript and web technologies and a deep understanding of the work of React.js and related technologies (Redux, MobX, and others).

**JavaScript**:

<details>
<summary>What types of data exist in JavaScript?</summary>
<div>
  <br/>
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

<details>
<summary>Whats is event loop in JavaScript and how it works?</summary>
<div>
  <br/>
  <p>JavaScript has a concurrency model based on an event loop, which is responsible for executing the code, collecting and processing events, and executing queued sub-tasks. This model is quite different from models in other languages like C and Java.</p>
  <img src="https://mdn.mozillademos.org/files/17124/The_Javascript_Runtime_Environment_Example.svg" />
  <h5>Stack</h5>
  <p>Function calls form a stack of frames.</p>
  <p>

    function foo(b) {
      let a = 10
      return a + b + 11
    }

    function bar(x) {
      let y = 3
      return foo(x * y)
    }

    console.log(bar(7)) //returns 42
  </p>
  <p>
    When calling bar, a first frame is created containing bar's arguments and local variables. When bar calls foo, a second frame is created and pushed on top of the first one containing foo's arguments and local variables. When foo returns, the top frame element is popped out of the stack (leaving only bar's call frame). When bar returns, the stack is empty.
  </p>
  <h5>Heap</h5>
  <p>
    Objects are allocated in a heap which is just a name to denote a large (mostly unstructured) region of memory.
  </p>
  <h5>Queue</h5>
  <p>
    A JavaScript runtime uses a message queue, which is a list of messages to be processed. Each message has an associated function which gets called in order to handle the message. The processing of functions continues until the stack is once again empty. Then, the event loop will process the next message in the queue (if there is one).
  </p>
  <h5>Event loop</h5>
  <p>
    The event loop got its name because of how it's usually implemented, which usually resembles:
  </p>
  <p>

    while (queue.waitForMessage()) {
      queue.processNextMessage()
    }
  </p>
  <p>
    queue.waitForMessage() waits synchronously for a message to arrive (if one is not already available and waiting to be handled).
  </p>
  <p><i>Source: <a href ="https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop">MDN web docs</a></i></p>
</div>
</details>

<details>
<summary>What is closure in JavaScript?</summary>
<div>
  <br/>
  <p>
    A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
  </p>
  <p>Every closure has three scopes:</p>
  <ul>
    <li>Local Scope (Own scope)</li>
    <li>Outer Functions Scope</li>
    <li>Global Scope</li>
  </ul>
  <p>
    A common mistake is not realizing that, in the case where the outer function is itself a nested function, access to the outer function's scope includes the enclosing scope of the outer function—effectively creating a chain of function scopes. To demonstrate, consider the following example code.
  </p>
  <p>

    // global scope
    var e = 10;
    function sum(a){
      return function(b){
        return function(c){
          // outer functions scope
          return function(d){
            // local scope
            return a + b + c + d + e;
          }
        }
      }
    }

    console.log(sum(1)(2)(3)(4)); // log 20

    // You can also write without anonymous functions:

    // global scope
    var e = 10;
    function sum(a){
      return function sum2(b){
        return function sum3(c){
          // outer functions scope
          return function sum4(d){
            // local scope
            return a + b + c + d + e;
          }
        }
      }
    }

    var s = sum(1);
    var s1 = s(2);
    var s2 = s1(3);
    var s3 = s2(4);
    console.log(s3) //log 20
  </p>
  <p>
    In the example above, there's a series of nested functions, all of which have access to the outer functions' scope. In this context, we can say that closures have access to all outer function scopes.
  </p>
  <p><i>Source: <a href ="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures">MDN web docs</a></i></p>
</div>
</details>

<details>
<summary>How does the “this” keyword work?</summary>
<div>
  <br/>
  <p>
    A function's this keyword behaves a little differently in JavaScript compared to other languages. It also has some differences between strict mode and non-strict mode.
  </p>
  <ul>
    <li>
      <b>Global context:</b> In the global execution context (outside of any function), this refers to the global object whether in strict mode or not.
    </li>
    <li>
      <b>Function context:</b> Inside a function, the value of this depends on how the function is called.
      <p>Since the following code is not in strict mode, and because the value of this is not set by the call, this will default to the global object, which is window in a browser. 
        
        function f1() {
          return this;
        }

        // In a browser:
        f1() === window; // true

        // In Node:
        f1() === globalThis; // true

   </p>
      <p>
        In strict mode, however, if the value of this is not set when entering an execution context, it remains as undefined.
  
        function f2() {
          'use strict'; // see strict mode
          return this;
        }

        f2() === undefined; // true
   </p>
    </li>
    <li>
      <b>Class context:</b> The behavior of this in classes and functions is similar, since classes are functions under the hood. But there are some differences and caveats. Within a class constructor, this is a regular object. All non-static methods within the class are added to the prototype of this.
    </li>
    <li>
      <b>Derived classes:</b> Unlike base class constructors, derived constructors have no initial this binding. Calling  super() creates a this binding within the constructor and essentially has the effect of evaluating the following line of code, where Base is the inherited class. Derived classes must not return before calling super(), unless they return an Object or have no constructor at all. Referring to this before calling super() will throw an error.
    </li>
  </ul>
  <p><i>Source: <a href ="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this">MDN web docs</a></i></p>
</div>
</details>

<details>
<summary>What are promises in JavaScript?</summary>
<div>
  <br/>
  <p>
    The Promise object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.
  </p>
  <p>
    A Promise is in one of these states:
  </p>
  <ul>
    <li>
      <i>pending:</i> initial state, neither fulfilled nor rejected.
    </li>
    <li>
      <i>fulfilled:</i> meaning that the operation completed successfully.
    </li>
    <li>
      <i>rejected:</i> meaning that the operation failed.
    </li>
  </ul>
  <p>
    A pending promise can either be fulfilled with a value, or rejected with a reason (error). When either of these options happens, the associated handlers queued up by a promise's then method are called.
  </p>
  <p>
    As the Promise.prototype.then() and Promise.prototype.catch() methods return promises, they can be chained.
  </p>
  <img src="https://mdn.mozillademos.org/files/15911/promises.png"/>
  <p>
    The methods promise.then(), promise.catch(), and promise.finally() are used to associate further action with a promise that becomes settled. These methods also return a newly generated promise object, which can optionally be used for chaining; for example, like this:

    const myPromise = 
      (new Promise(myExecutorFunc))
      .then(handleFulfilledA,handleRejectedA)
      .then(handleFulfilledB,handleRejectedB)
      .then(handleFulfilledC,handleRejectedC);

    // or, perhaps better ...

    const myPromise =
      (new Promise(myExecutorFunc))
      .then(handleFulfilledA)
      .then(handleFulfilledB)
      .then(handleFulfilledC)
      .catch(handleRejectedAny);
  </p>
  <p><i>Source: <a href ="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">MDN web docs</a></i></p>
</div>
</details>

<br/>

**React**:

<details>
<summary>What component life cycle methods exist in React?</summary>
<div>
  <br/>
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
  <p><i>Source: <a href ="https://reactjs.org/docs/react-component.html#render">reactjs.org</a></i></p>
</div>
</details>

<details>
<summary>What is Context in React?</summary>
<div>
  <br />
  <p>Context is designed to share data that can be considered “global” for a tree of React components, such as the current authenticated user, theme, or preferred language.</p>
  <p>Using context, we can avoid passing props through intermediate elements:
    
    // Context lets us pass a value deep into the component tree
    // without explicitly threading it through every component.
    // Create a context for the current theme (with "light" as the default).
    const ThemeContext = React.createContext('light');

    class App extends React.Component {
      render() {
        // Use a Provider to pass the current theme to the tree below.
        // Any component can read it, no matter how deep it is.
        // In this example, we're passing "dark" as the current value.
        return (
          <ThemeContext.Provider value="dark">
            <Toolbar />
          </ThemeContext.Provider>
        );
      }
    }

    // A component in the middle doesn't have to
    // pass the theme down explicitly anymore.
    function Toolbar() {
      return (
        <div>
          <ThemedButton />
        </div>
      );
    }

    class ThemedButton extends React.Component {
      // Assign a contextType to read the current theme context.
      // React will find the closest theme Provider above and use its value.
      // In this example, the current theme is "dark".
      static contextType = ThemeContext;
      render() {
        return <Button theme={this.context} />;
      }
    }
  </p>
  <p>Context is primarily used when some data needs to be accessible by many components at different nesting levels. Apply it sparingly because it makes component reuse more difficult.</p>
  <ul>
    <b>API:</b>
    <li>
      <b>React.createContext</b> - creates a Context object. When React renders a component that subscribes to this Context object it will read the current context value from the closest matching Provider above it in the tree.
    </li>
    <li>
      <b>Context.Provider</b> - every Context object comes with a Provider React component that allows consuming components to subscribe to context changes.
    </li>
    <li>
      <b>Class.contextType</b> - the contextType property on a class can be assigned a Context object created by React.createContext(). This lets you consume the nearest current value of that Context type using this.context. You can reference this in any of the lifecycle methods including the render function.
    </li>
    <li>
      <b>Context.Consumer</b> - a React component that subscribes to context changes. This lets you subscribe to a context within a function component. Requires a function as a child. The function receives the current context value and returns a React node. The value argument passed to the function will be equal to the value prop of the closest Provider for this context above in the tree. If there is no Provider for this context above, the value argument will be equal to the defaultValue that was passed to createContext().
    </li>
    <li>
      <b>Context.displayName</b> - Context object accepts a displayName string property. React DevTools uses this string to determine what to display for the context.
    </li>
  </ul>
  <p><i>Source: <a href ="https://reactjs.org/docs/context.html">reactjs.org</a></i></p>
</div>
</details>

<details>
<summary>What is the Virtual DOM?</summary>
<div>
  <br/>
  <p>
    The virtual DOM (VDOM) is a programming concept where an ideal, or “virtual”, representation of a UI is kept in memory and synced with the “real” DOM by a library such as ReactDOM. This process is called reconciliation.
  </p>
  <p>
    In React world, the term “virtual DOM” is usually associated with React elements since they are the objects representing the user interface. React, however, also uses internal objects called “fibers” to hold additional information about the component tree. They may also be considered a part of “virtual DOM” implementation in React.
  </p>
  <p><i>Source: <a href ="https://reactjs.org/docs/faq-internals.html#what-is-the-virtual-dom">reactjs.org</a></i></p>
</div>
</details>

<details>
<summary>Why do you need the key attribute when rendering lists?</summary>
<div>
  <br/>
  <p>
    Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity
  </p>
  <p>
    The best way to pick a key is to use a string that uniquely identifies a list item among its siblings. Most often you would use IDs from your data as keys
  </p>
  <p>
    When you don’t have stable IDs for rendered items, you may use the item index as a key as a last resort. We don’t recommend using indexes for keys if the order of items may change. This can negatively impact performance and may cause issues with component state.
  </p>
  <p><i>Source: <a href ="https://reactjs.org/docs/lists-and-keys.html#keys">reactjs.org</a></i></p>
</div>
</details>

<details>
<summary>How does "children" prop work?</summary>
<div>
  <br/>
  <p>
    Some components don’t know their children ahead of time. This is especially common for components like Sidebar or Dialog that represent generic “boxes”. We recommend that such components use the special children prop to pass children elements directly into their output:
  </p>
  <p>

      function FancyBorder(props) {
        return (
          <div className={'FancyBorder FancyBorder-' + props.color}>
            {props.children}
          </div>
        );
      }
  </p>
  <p>
    This lets other components pass arbitrary children to them by nesting the JSX:
  </p>
  <p>

      function WelcomeDialog() {
        return (
          <FancyBorder color="blue">
            <h1 className="Dialog-title">
              Welcome
            </h1>
            <p className="Dialog-message">
              Thank you for visiting our spacecraft!
            </p>
          </FancyBorder>
        );
      }
  </p>
  <p>
    Anything inside the <FancyBorder> JSX tag gets passed into the FancyBorder component as a children prop. Since FancyBorder renders {props.children} inside a div, the passed elements appear in the final output.
  </p>
  <p><i>Source: <a href ="https://reactjs.org/docs/composition-vs-inheritance.html#containment">reactjs.org</a></i></p>
</div>
</details>


<details>
<summary>What is the difference between controlled and uncontrolled components?</summary>
<div>
  <br/>
  <p>
    In HTML, form elements such as input, textarea, and select typically maintain their own state and update it based on user input. In React, mutable state is typically kept in the state property of components, and only updated with setState().
  </p>
  <p>
    We can combine the two by making the React state be the “single source of truth”. Then the React component that renders a form also controls what happens in that form on subsequent user input. An input form element whose value is controlled by React in this way is called a <b>“controlled component”</b>.
  </p>
  <p>
    To write an <b>uncontrolled component</b>, instead of writing an event handler for every state update, you can use a ref to get form values from the DOM.
  </p>
  <p>
    Since an uncontrolled component keeps the source of truth in the DOM, it is sometimes easier to integrate React and non-React code when using uncontrolled components. It can also be slightly less code if you want to be quick and dirty. Otherwise, you should usually use controlled components.
  </p>
  <p><i>Source: 
    <a href ="https://reactjs.org/docs/forms.html#controlled-components">reactjs.org</a>,
    <a href ="https://reactjs.org/docs/uncontrolled-components.html">reactjs.org</a>
  </i></p>
</div>
</details>

<details>
<summary>What is PureComponent?</summary>
<div>
  <br/>
  <p>
    React.PureComponent is similar to React.Component. The difference between them is that React.Component doesn’t implement shouldComponentUpdate(), but React.PureComponent implements it with a shallow prop and state comparison.
  </p>
  <p>
    If your React component’s render() function renders the same result given the same props and state, you can use React.PureComponent for a performance boost in some cases.
  </p>
  <p>
    React.PureComponent’s shouldComponentUpdate() only shallowly compares the objects. If these contain complex data structures, it may produce false-negatives for deeper differences. Only extend PureComponent when you expect to have simple props and state, or use forceUpdate() when you know deep data structures have changed. Or, consider using immutable objects to facilitate fast comparisons of nested data. Furthermore, React.PureComponent’s shouldComponentUpdate() skips prop updates for the whole component subtree. Make sure all the children components are also “pure”.
  </p>
  <p><i>Source: 
    <a href ="https://reactjs.org/docs/react-api.html#reactpurecomponent">reactjs.org</a>
  </i></p>
</div>
</details>

<br/>

**Web technologies**:

<details>
<summary>What is HTTP?</summary>
<div>
  <br/>
  <p>
    HTTP is a protocol which allows the fetching of resources, such as HTML documents. It is the foundation of any data exchange on the Web and it is a client-server protocol, which means requests are initiated by the recipient, usually the Web browser. A complete document is reconstructed from the different sub-documents fetched, for instance text, layout description, images, videos, scripts, and more.
  </p>
  <img src="https://mdn.mozillademos.org/files/13677/Fetching_a_page.png"/>
  <p>
    Here is a list of common features controllable with HTTP:
  </p>
  <ul>
    <li>
      <b>Caching</b> - How documents are cached can be controlled by HTTP. The server can instruct proxies and clients, about what to cache and for how long. The client can instruct intermediate cache proxies to ignore the stored document.
Relaxing the origin constraint
    </li>
    <li>
      <b>Relaxing the origin constraint</b> - To prevent snooping and other privacy invasions, Web browsers enforce strict separation between Web sites. Only pages from the same origin can access all the information of a Web page. Though such constraint is a burden to the server, HTTP headers can relax this strict separation on the server side, allowing a document to become a patchwork of information sourced from different domains; there could even be security-related reasons to do so.
    </li>
    <li>
      <b>Authentication</b> - Some pages may be protected so that only specific users can access them. Basic authentication may be provided by HTTP, either using the WWW-Authenticate and similar headers, or by setting a specific session using HTTP cookies.
    </li>
    <li>
      <b>Proxy and tunneling</b> - Servers or clients are often located on intranets and hide their true IP address from other computers. HTTP requests then go through proxies to cross this network barrier. Not all proxies are HTTP proxies. The SOCKS protocol, for example, operates at a lower level. Other protocols, like ftp, can be handled by these proxies.
    </li>
    <li>
      <b>Sessions</b> - Using HTTP cookies allows you to link requests with the state of the server. This creates sessions, despite basic HTTP being a state-less protocol. This is useful not only for e-commerce shopping baskets, but also for any site allowing user configuration of the output.
    </li>
  </ul>
  <p><i>Source: <a href ="https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview">MDN web docs</a></i></p>
</div>
</details>
