# redux-websocket-middleware

Redux middleware that handles pure websockets


Example: creating actions that dispatch to a websocket:

```js
import {WebsocketActionTypes} from 'redux-websocket-middleware'

function writeToSocket(data) {
  return {
    type: WebsocketActionTypes.SEND,
    payload: data
  }
}
```

Example: listening for data received from the websocket.
Data received from the socket will dispatch an action of `WebsocketActionTypes.RECEIVE`. 

```js
import { WebsocketActionTypes } from "redux-websocket-middleware"

function reducer (state, action) {
  if (action.type === WebsocketActionTypes.RECEIVED) {
    // ...
  }
}
```

### installation and endpoint configuration

reduxWebsocketMiddleware is added as middleware in the standard redux pattern:

```js
import { applyMiddleware, createStore }
import { reduxWebsocketMiddleware } from "redux-websocket-middleware"
import reducer from "./reducer"

const endpoint = 'ws://echo.websocket.org' // or desired endpoint

const socketMiddleware = reduxWebsocketMiddleware(endpoint)

const middleware = applyMiddleware(socketMiddleware)

const store = createStore(reducer, middleware)
```

