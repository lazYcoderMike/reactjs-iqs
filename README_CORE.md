
<div>
<p align="center">
  <a href=https://react.gg/?s=rjsiq>
    <img src="./images/collab/uidev-banner4x.png" alt="React interview" width="100%">
  </a>
</p>
</div>



<div>
<p align="center">
  <a href=https://zerotomastery.io/?utm_source=github&utm_medium=sponsor&utm_campaign=reactjs-interview-questions>
    <img src=https://process.fs.teachablecdn.com/ADNupMnWyR7kCWRvm76Laz/resize=height:70/https://www.filepicker.io/api/file/AKYtjj5SSGyJuyZrkAB2 alt="ZTM Logo" width="100" height="50">
  </a>
    <ol>
      <li>I recommend this <a href="https://links.zerotomastery.io/react_sudheer">React course</a> if you’re serious about learning React and want to go beyond the basics</li>
      <li>Want to ace your coding interview and get hired at your dream company? <a href="http://links.zerotomastery.io/mci_sudheer">Take this coding interview bootcamp</a></li>
    </ol>
  </p>
</div>

| No. | Questions                                                                                                                                                                                                                        |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|     | **Core React Router**        

| 129 | [What is React Router?](#what-is-react-router)                                                                                                                                                                                   |
| 130 | [How React Router is different from history library?](#how-react-router-is-different-from-history-library)                                                                                                                       |
| 131 | [What are the \<Router> components of React Router v4?](#what-are-the-router-components-of-react-router-v4)                                                                                                                      |
| 132 | [What is the purpose of push and replace methods of history?](#what-is-the-purpose-of-push-and-replace-methods-of-history)                                                                                                       |
| 133 | [How do you programmatically navigate using React router v4?](#how-do-you-programmatically-navigate-using-react-router-v4)                                                                                                       |
| 134 | [How to get query parameters in React Router v4](#how-to-get-query-parameters-in-react-router-v4)                                                                                                                                |
| 135 | [Why you get "Router may have only one child element" warning?](#why-you-get-router-may-have-only-one-child-element-warning)                                                                                                     |
| 136 | [How to pass params to history.push method in React Router v4?](#how-to-pass-params-to-historypush-method-in-react-router-v4)                                                                                                    |
| 137 | [How to implement default or NotFound page?](#how-to-implement-default-or-notfound-page)                                                                                                                                         |
| 138 | [How to get history on React Router v4?](#how-to-get-history-on-react-router-v4)                                                                                                                                                 |
| 139 | [How to perform automatic redirect after login?](#how-to-perform-automatic-redirect-after-login)

129. ### What is React Router?

     React Router is a powerful routing library built on top of React that helps you add new screens and flows to your application incredibly quickly, all while keeping the URL in sync with what's being displayed on the page.

**[⬆ Back to Top](#table-of-contents)**

130. ### How React Router is different from history library?

     React Router is a wrapper around the `history` library which handles interaction with the browser's `window.history` with its browser and hash histories. It also provides memory history which is useful for environments that don't have global history, such as mobile app development (React Native) and unit testing with Node.

**[⬆ Back to Top](#table-of-contents)**

131. ### What are the `<Router>` components of React Router v4?

     React Router v4 provides below 3 `<Router>` components:

     1. `<BrowserRouter>`
     2. `<HashRouter>`
     3. `<MemoryRouter>`

     The above components will create _browser_, _hash_, and _memory_ history instances. React Router v4 makes the properties and methods of the `history` instance associated with your router available through the context in the `router` object.

**[⬆ Back to Top](#table-of-contents)**

132. ### What is the purpose of `push()` and `replace()` methods of `history`?

     A history instance has two methods for navigation purpose.

     1. `push()`
     2. `replace()`

     If you think of the history as an array of visited locations, `push()` will add a new location to the array and `replace()` will replace the current location in the array with the new one.

**[⬆ Back to Top](#table-of-contents)**

133. ### How do you programmatically navigate using React Router v4?

     There are three different ways to achieve programmatic routing/navigation within components.

     1. **Using the `withRouter()` higher-order function:**

        The `withRouter()` higher-order function will inject the history object as a prop of the component. This object provides `push()` and `replace()` methods to avoid the usage of context.

        ```jsx harmony
        import { withRouter } from "react-router-dom"; // this also works with 'react-router-native'

        const Button = withRouter(({ history }) => (
          <button
            type="button"
            onClick={() => {
              history.push("/new-location");
            }}
          >
            {"Click Me!"}
          </button>
        ));
        ```

     2. **Using `<Route>` component and render props pattern:**

        The `<Route>` component passes the same props as `withRouter()`, so you will be able to access the history methods through the history prop.

        ```jsx harmony
        import { Route } from "react-router-dom";

        const Button = () => (
          <Route
            render={({ history }) => (
              <button
                type="button"
                onClick={() => {
                  history.push("/new-location");
                }}
              >
                {"Click Me!"}
              </button>
            )}
          />
        );
        ```

     3. **Using context:**

        This option is not recommended and treated as unstable API.

        ```jsx harmony
        const Button = (props, context) => (
          <button
            type="button"
            onClick={() => {
              context.history.push("/new-location");
            }}
          >
            {"Click Me!"}
          </button>
        );

        Button.contextTypes = {
          history: React.PropTypes.shape({
            push: React.PropTypes.func.isRequired,
          }),
        };
        ```

**[⬆ Back to Top](#table-of-contents)**

134. ### How to get query parameters in React Router v4?

     The ability to parse query strings was taken out of React Router v4 because there have been user requests over the years to support different implementation. So the decision has been given to users to choose the implementation they like. The recommended approach is to use query strings library.

     ```javascript
     const queryString = require("query-string");
     const parsed = queryString.parse(props.location.search);
     ```

     You can also use `URLSearchParams` if you want something native:

     ```javascript
     const params = new URLSearchParams(props.location.search);
     const foo = params.get("name");
     ```

     You should use a _polyfill_ for IE11.

**[⬆ Back to Top](#table-of-contents)**

135. ### Why you get "Router may have only one child element" warning?

     You have to wrap your Route's in a `<Switch>` block because `<Switch>` is unique in that it renders a route exclusively.

     At first you need to add `Switch` to your imports:

     ```javascript
     import { Switch, Router, Route } from "react-router";
     ```

     Then define the routes within `<Switch>` block:

     ```jsx harmony
     <Router>
       <Switch>
         <Route {/* ... */} />
         <Route {/* ... */} />
       </Switch>
     </Router>
     ```

**[⬆ Back to Top](#table-of-contents)**

136. ### How to pass params to `history.push` method in React Router v4?

     While navigating you can pass props to the `history` object:

     ```javascript
     this.props.history.push({
       pathname: "/template",
       search: "?name=sudheer",
       state: { detail: response.data },
     });
     ```

     The `search` property is used to pass query params in `push()` method.

**[⬆ Back to Top](#table-of-contents)**

137. ### How to implement _default_ or _NotFound_ page?

     A `<Switch>` renders the first child `<Route>` that matches. A `<Route>` with no path always matches. So you just need to simply drop path attribute as below

     ```jsx harmony
     <Switch>
       <Route exact path="/" component={Home} />
       <Route path="/user" component={User} />
       <Route component={NotFound} />
     </Switch>
     ```

**[⬆ Back to Top](#table-of-contents)**

138. ### How to get history on React Router v4?

     Below are the list of steps to get history object on React Router v4,

     1. Create a module that exports a `history` object and import this module across the project.

        For example, create `history.js` file:

        ```javascript
        import { createBrowserHistory } from "history";

        export default createBrowserHistory({
          /* pass a configuration object here if needed */
        });
        ```

     2. You should use the `<Router>` component instead of built-in routers. Import the above `history.js` inside `index.js` file:

        ```jsx harmony
        import { Router } from "react-router-dom";
        import history from "./history";
        import App from "./App";

        ReactDOM.render(
          <Router history={history}>
            <App />
          </Router>,
          holder
        );
        ```

     3. You can also use push method of `history` object similar to built-in history object:

        ```javascript
        // some-other-file.js
        import history from "./history";

        history.push("/go-here");
        ```

**[⬆ Back to Top](#table-of-contents)**

139. ### How to perform automatic redirect after login?

     The `react-router` package provides `<Redirect>` component in React Router. Rendering a `<Redirect>` will navigate to a new location. Like server-side redirects, the new location will override the current location in the history stack.

     ```javascript
     import React, { Component } from "react";
     import { Redirect } from "react-router";

     export default class LoginComponent extends Component {
       render() {
         if (this.state.isLoggedIn === true) {
           return <Redirect to="/your/redirect/page" />;
         } else {
           return <div>{"Login Please"}</div>;
         }
       }
     }
     ```
