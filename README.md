# redux-websocket-middleware

Redux middleware that handles pure websockets

This middleware is used to send and receive websocket messages over pure websockets using Redux actions and reducers.  

Once installed as redux middleware and endpoint configured, any action of type: WebsocketActionTypes.SEND will have its payload sent over websockets to the endpoint.

For example, an action creator function to send its data to through the websocket:

```js
import {WebsocketActionTypes} from 'redux-websocket-middleware'

function websocketSendAction(data) {
  return {
    type: WebsocketActionTypes.SEND,
    payload: data
  }
}
```

Data received over websockets from the endpoint will dispatch an action of type `WebsocketActionTypes.RECEIVE`. 
The following is an example reducer that listens for data received from the websocket:

```js
import { WebsocketActionTypes } from "redux-websocket-middleware"

function reducer (state, action) {
  if (action.type === WebsocketActionTypes.RECEIVE) {
    // ...
  }
}
```

### installation and endpoint configuration

reduxWebsocketMiddleware is added as middleware following the standard redux pattern.
The endpoint URL is specified when creating the middleware:

```js
import { applyMiddleware, createStore }
import { reduxWebsocketMiddleware } from "redux-websocket-middleware"
import reducer from "./reducer"

const endpoint = 'ws://echo.websocket.org' // or desired endpoint

const websocketMiddleware = reduxWebsocketMiddleware(endpoint)

const middleware = applyMiddleware(websocketMiddleware)

const store = createStore(reducer, middleware)
```

