# redux-websocket-middleware

Redux middleware that handles pure websockets


Example: creating actions that dispatch to a websocket:

```js
import {WebsocketActionTypes} from 'redux-websocket-middleware'

function websocketSendAction(data) {
  return {
    type: WebsocketActionTypes.SEND,
    payload: data
  }
}
```

Example: listening for data received from the websocket.
Data received from the websocket will dispatch an action of `WebsocketActionTypes.RECEIVE`. 

```js
import { WebsocketActionTypes } from "redux-websocket-middleware"

function reducer (state, action) {
  if (action.type === WebsocketActionTypes.RECEIVE) {
    // ...
  }
}
```

### installation and endpoint configuration

reduxWebsocketMiddleware is added as middleware in the standard redux pattern.
The endpoint URL is specified when instantiating the middleware:

```js
import { applyMiddleware, createStore }
import { reduxWebsocketMiddleware } from "redux-websocket-middleware"
import reducer from "./reducer"

const endpoint = 'ws://echo.websocket.org' // or desired endpoint

const websocketMiddleware = reduxWebsocketMiddleware(endpoint)

const middleware = applyMiddleware(websocketMiddleware)

const store = createStore(reducer, middleware)
```

