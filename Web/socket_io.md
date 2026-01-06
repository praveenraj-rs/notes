
In Server (Nodejs)
```
npm install socket.io
```

In Client (React)
```
npm install socket.io-client
```


### Integrating Socket.IO

```js
const express = require('express');
const http = require('http');
const path = require('path');
const { Server } = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = new Server(server,{
cors:
{origin:"http://localhost:3000",methods:["GET", "POST"],}
}
);

app.get('/', (req, res) => {
  res.sendFile(join(__dirname, 'index.html'));
});

io.on('connection', (socket) => {
  console.log(`a user connected: ${socket.id}`);
});

server.listen(3000, () => {
  console.log('server running at http://localhost:3000');
});
```

### Connected and Disconnected

```js
io.on('connection', (socket) => {
  console.log(`a user connected ${socket.id}`);
  socket.on('disconnect', () => {
    console.log(`user disconnected ${socket.id}`);
  });
});
```


### Getting API Call on 10 second Interval

```js

let interval;
io.on(“connection”, (socket) => {  
	 console.log(`New client connected: ${socket.id}`);  
	 if (interval) {  
		 clearInterval(interval);
		 }  
	 interval = setInterval(() => getApiAndEmit(socket), 10000);  
	 socket.on(“disconnect”, () => {  
		 console.log(“Client disconnected”);  
		 });  
});
```

Complete Server Side Code for fetching real-time temp:

```js
const express = require("express");  
const cors = require("cors");
const http = require("http");  
const {Server} = require("socket.io");  
const axios = require("axios");
const port = process.env.PORT || 3000;

const app = express();
app.use(cors());
const server = http.createServer(app);  
const io = Server(server,{
cors:
{
origin:"http://localhost:3000",
methods:["GET", "POST"],
}
});


let interval;
io.on(“connection”, (socket) => {  
	 console.log(`New client connected: ${socket.id}`);  
	 if (interval) {  
		 clearInterval(interval);
		 }  
	 interval = setInterval(() => getApiAndEmit(socket), 10000);  
	 socket.on(“disconnect”, () => {  
		 console.log(“Client disconnected”);  
		 });  
});

const getApiAndEmit = async socket => {  
  try {  
    const res = await axios.get(     "https://api.darksky.net/forecast/PUT_YOUR_API_KEY_HERE/43.7695,11.2558);  
    socket.emit("FromAPI", res.data.currently.temperature);  
  } 
  catch (error) {  
    console.error(`Error: ${error.code}`);  
  }  
};
app.listen(port, () => console.log(`Listening on port ${port}`));
```

Client Side Code

```js
import React, { Component } from "react";  
import socketIOClient from "socket.io-client";

class App extends Component {  
  constructor() {  
    super();  
    this.state = {  
      response: false,  
      endpoint: "[http://127.0.0.1:4001](http://127.0.0.1:4001/)"  
    };  
  }componentDidMount() {  
    const { endpoint } = this.state;  
    const socket = socketIOClient(endpoint);  
    socket.on("FromAPI", data => this.setState({ response: data }));  
  }render() {  
    const { response } = this.state;  
    return (  
      <div style={{ textAlign: "center" }}>  
        {response  
          ? <p>  
              The temperature in Florence is: {response} °F  
            </p>  
          : <p>Loading...</p>}  
      </div>  
    );  
  }  
}export default App;
```

## Real-Time Toggle Switch Example

#### Nodejs

```js
// server.js
const http = require("http");
const express = require("express");
const socketIo = require("socket.io");
const cors = require("cors");
const app = express();
app.use(cors());
const server = http.createServer(app);
const io = socketIo(server, {
  cors: {
    origin: "*",
  },
});

io.on("connection", (socket) => {
  console.log("A client connected");

  // Handle state change events from clients
  socket.on("stateChange", (newState) => {
    // Broadcast the state change to all connected clients, including the sender
    io.emit("updateState", newState);
  });

  // Handle disconnection events
  socket.on("disconnect", () => {
    console.log("A client disconnected");
  });
});

const PORT = 3001;

server.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});

```

#### React

```js
// ToggleSwitch.js
import React, { useEffect, useState } from "react";
import io from "socket.io-client";

const ToggleSwitch = () => {
  const [isToggled, setToggled] = useState(() => {
    // Initialize the state from local storage or default to false
    const storedState = localStorage.getItem("toggleState");
    return storedState ? JSON.parse(storedState) : false;
  });
  const [socket, setSocket] = useState(null);

  useEffect(() => {
    const socketConnection = io("http://localhost:3001"); // Replace with your server URL
    setSocket(socketConnection);

    socketConnection.on("connect", () => {
      console.log("Connected to the server");
      // Emit the current state to ensure synchronization after a refresh
      socketConnection.emit("stateChange", isToggled);
    });

    socketConnection.on("updateState", (newState) => {
      setToggled(newState);
      // Save the updated state to local storage
      localStorage.setItem("toggleState", JSON.stringify(newState));
    });

    // Clean up when the component unmounts
    return () => {
      if (socketConnection) {
        socketConnection.disconnect();
      }
    };
  }, [isToggled]);

  const handleToggle = () => {
    if (socket) {
      const newState = !isToggled;
      setToggled(newState);

      // Emit a state change event to the server
      socket.emit("stateChange", newState);
      // Save the updated state to local storage
      localStorage.setItem("toggleState", JSON.stringify(newState));
    }
  };

  return (
    <div>
      <label>
        Toggle Switch
        <input type="checkbox" checked={isToggled} onChange={handleToggle} />
      </label>
    </div>
  );
};

export default ToggleSwitch;

```


### Chat Application

#### Storing the userState

```js
const UsersState = {
    users: [],
    setUsers: function (newUsersArray) {
        this.users = newUsersArray
    }
}
```