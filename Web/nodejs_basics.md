NodeJS Basics

### Commands
- sudo npm install npm -g
- npm --version
- npm init
- npm install nodemon
- npm install nodemon -g
- npm install nodemon -D
- npm ls
- npm ls -g
- npm uninstall nodemon
- npm search nodemon
- npm publish
- path.parse(filepath)
- fs.readFileSync('text.txt')
- fs.readFile('text.txt',(err,data)=>{console.log(data.toString())})
- fs.exitsSync('./new');
- fs.mkdir('./new');
- fs.rmdir('./new');
- npm install date-fns
- Date()
- new Date()
- const {format} = require("date-fns"}
- format(new Date(), 'dd/MM/yyyy  HH:mm:ss')
- const express = require('express')
- const app = express()
- require('crypto').randomBytes(64).toString('hex')
- .help
- .save
- .load
- import express from "express"
- import path from "path"
- import {Server} from "socket.io"
- `import { fileURLToPath } from 'url'`
- `const __filename = fileURLToPath(import.meta.url)`
- `const __dirname = path.dirname(__filename)`
- `app.use(express.static(path.join(__dirname, "public")))`
- 
```sh
# installs NVM (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
# download and install Node.js
nvm install 20
# verifies the right Node.js version is in the environment
node -v # should print `v20.11.1`
# verifies the right NPM version is in the environment
npm -v # should print `10.2.4`
```
- `node --env-file=.env app.js`
- process.env.NAME

### Simple Server
```js
const http = require("http");

http
  .createServer((req, res) => {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Hello World\n");
  })
  .listen(8000);

console.log("Server running at http://127.0.0.1:8081/");
```

### fs.readFileSync
```js
const fs = require("fs");
const data = fs.readFileSync("./text.txt");
console.log(data.toString());
console.log("Program Ended");
```

### fs.readFile
```js
var fs = require("fs");

fs.readFile("input.txt", function (err, data) {
  if (err) return console.error(err);
  console.log(data.toString());
});

console.log("Program Ended");
```

### File Stream
```js
rs = fs.createReadStream('fileName.txt',{encodeing:'utf8'});
ws = fs.createWriteStream('newFile.txt');

rs.on('data',(dataChunk)=>{ws.write(dataChunk)});
or
rs.pipe(ws);
```

### Event Loop
```js
// Import events module
var events = require("events");

// Create an eventEmitter object
var eventEmitter = new events.EventEmitter();

// Create an event handler as follows
var connectHandler = function connected() {
  console.log("connection succesful.");

  // Fire the data_received event
  eventEmitter.emit("data_received");
};

// Bind the connection event with the handler
eventEmitter.on("connection", connectHandler);

// Bind the data_received event with the anonymous function
eventEmitter.on("data_received", function () {
  console.log("data received succesfully.");
});

// Fire the connection event
eventEmitter.emit("connection");

console.log("Program Ended.");
```

### Express
- const express = require('express')
- const app = express()
```js
app.get('/',(req,res)={res.send('Hello World!')})
app.listen(8000)
```

```js
app.get('^/$|index(.html)?',(req,res)={res.send('Hello World!')})
app.listen(8000)
```

```js
app.get('/',(req,res)=>{res.sendFile(path.join(_dirname,'index.html'))})
```

```js
app.get("^/$|old_page(.html)?", (req, res) => { res.redirect(301, path.join(__dirname, "login", "index.html"));}); //302 by default
```

```js
app.get("^/$|old_page(.html)?", (req, res) => { 
res.status(404).sendFile(path.join(__dirname, "login", "404.html"));});
```

#### Nested function in Express
```js
app.get("/demo(.html)?", (req, res, next) => {
console.log("Hello World!");
next();
},
(req, res) => {
res.send("Hello World");
});
```

#### Nested Function 2 in Express
```js
const one = (req, res, next) => {
  console.log("one");
  next();
};
const two = (req, res, next) => {
  console.log("two");
  next();
};

const three = (req, res, next) => {
  console.log("three");
  res.send("Three");
};

app.get("/demo(.html)?", [one, two, three]);
```

#### Builtin Middle-wares
```js
app.use(express.urlencoded({ extended: false })); 
app.use(express.json());
app.use(express.static (path.join(_dirname, '/public')));
```

### Basic Logger
```js
const fs = require("fs");
const path = require("path");
const { format } = require("date-fns");
const { v4: uuid } = require("uuid");

const logger = (req, res, next) => {
  const date = format(new Date(), "dd:MM:yyyy|HH:mm:ss");
  const id = uuid();
  fs.appendFileSync(
    path.join(__dirname, "..", "log", "logEvents.txt"),
    `${date}\t${id}\t${req.method}\t${req.path}\t${req.headers.origin}\n`);
  next();
};
module.exports = logger;
```

#### Middle-ware
Using the above the logger function as middle-ware
```js
const logger = require('./log/logger')
const express = require('express');
const app = express();

app.use(logger)
```

### CORS 

```js
const cors = require('cors')
// Cross Origin Resource Sharing
const whitelist = ['https://www.yoursite.com','http://127.0.0.1:5500','http://localhost:3500']
const corsOptions { origin: (origin, callback) => {
if (whitelist.indexOf(origin) !== -1) {
callback(null, true)
} 
else { callback(new Error('Not allowed by CORS'));}
},
optionsSuccessStatus: 200
}

app.use(cors (corsoptions));
```

### app.all
```js
app.all('*', (req, res) => {
res.status (404);
if (req.accepts('html')) {
res.sendFile(path.join(_dirname, 'views', '404.html'));
} else if (req.accepts('json')) {
res.json({ error: "404 Not Found" });
} else {
res.type('txt').send("404 Not Found");
});
```

### Routers
```js
const path = require("path");
const express = require("express");
const router = express.Router();

router.get("^/$|index(.html)?", (req, res) => {
  res.sendFile(path.join(__dirname, "..", "login", "subLogin", "index.html"));
});

router.get("^/$|test(.html)?", (req, res) => {
  res.sendFile(path.join(__dirname, "..", "login", "subLogin", "test.html"));
});

module.exports = router;
```

#### In server.js
```js
app.use("/subDir", express.static(path.join(__dirname, "login")));
app.use("/subDir", require("./routers/subRoutes"));
```

#### Get, Post, Put, Delete requests
```js
const express = require("express");
const router = express.Router();
const data = {};
data.employees = require("../../data/employees.json");
router
  .route("/")
  .get((req, res) => {
    res.json(data.employees);
  })
  .post((req, res) => {
    res.json({
      firstname: req.body.firstname,
      lastname: req.body.lastname,
    });
  })
  .put((req, res) => {
    res.json({
      firstname: req.body.firstname,
      lastname: req.body.lastname,
    });
  })
  .delete((req, res) => {
    res.json({ id: req.body.id });
  });

router.route("/:id").get((req, res) => {
  res.json({ id: req.params.id });
});

module.exports = router;
```

### Controllers
#### registerController 
```js
const usersDB = {
  users: require("../model/users.json"),
  setUsers: function (data) {
    this.users = data;
  },
};
const fsPromises = require("fs").promises;
const path = require("path");
const bcrypt = require("bcrypt");

const handleNewUser = async (req, res) => {
  const { user, pwd } = req.body;
  if (!user || !pwd)
    return res
      .status(400)
      .json({ message: "Username and password are required." });
  // check for duplicate usernames in the db
  const duplicate = usersDB.users.find((person) => person.username === user);
  if (duplicate) return res.sendStatus(409); //Conflict
  try {
    //encrypt the password
    const hashedPwd = await bcrypt.hash(pwd, 10);
    //store the new user
    const newUser = { username: user, password: hashedPwd };
    usersDB.setUsers([...usersDB.users, newUser]);
    await fsPromises.writeFile(
      path.join(__dirname, "..", "model", "users.json"),
      JSON.stringify(usersDB.users)
    );
    console.log(usersDB.users);
    res.status(201).json({ success: `New user ${user} created!` });
  } catch (err) {
    res.status(500).json({ message: err.message });
  }
};

module.exports = { handleNewUser };
```

#### authController
```js
const usersDB = {
    users: require('../model/users.json'),
    setUsers: function (data) { this.users = data }
}
const bcrypt = require('bcrypt');

const handleLogin = async (req, res) => {
    const { user, pwd } = req.body;
    if (!user || !pwd) return res.status(400).json({ 'message': 'Username and password are required.' });
    const foundUser = usersDB.users.find(person => person.username === user);
    if (!foundUser) return res.sendStatus(401); //Unauthorized 
    // evaluate password 
    const match = await bcrypt.compare(pwd, foundUser.password);
    if (match) {
        // create JWTs
        res.json({ 'success': `User ${user} is logged in!` });
    } else {
        res.sendStatus(401);
    }
}

module.exports = { handleLogin };
```

#### employeesController
```js
const data = {
    employees: require('../model/employees.json'),
    setEmployees: function (data) { this.employees = data }
}

const getAllEmployees = (req, res) => {
    res.json(data.employees);
}

const createNewEmployee = (req, res) => {
    const newEmployee = {
        id: data.employees?.length ? data.employees[data.employees.length - 1].id + 1 : 1,
        firstname: req.body.firstname,
        lastname: req.body.lastname
    }

    if (!newEmployee.firstname || !newEmployee.lastname) {
        return res.status(400).json({ 'message': 'First and last names are required.' });
    }

    data.setEmployees([...data.employees, newEmployee]);
    res.status(201).json(data.employees);
}

const updateEmployee = (req, res) => {
    const employee = data.employees.find(emp => emp.id === parseInt(req.body.id));
    if (!employee) {
        return res.status(400).json({ "message": `Employee ID ${req.body.id} not found` });
    }
    if (req.body.firstname) employee.firstname = req.body.firstname;
    if (req.body.lastname) employee.lastname = req.body.lastname;
    const filteredArray = data.employees.filter(emp => emp.id !== parseInt(req.body.id));
    const unsortedArray = [...filteredArray, employee];
    data.setEmployees(unsortedArray.sort((a, b) => a.id > b.id ? 1 : a.id < b.id ? -1 : 0));
    res.json(data.employees);
}

const deleteEmployee = (req, res) => {
    const employee = data.employees.find(emp => emp.id === parseInt(req.body.id));
    if (!employee) {
        return res.status(400).json({ "message": `Employee ID ${req.body.id} not found` });
    }
    const filteredArray = data.employees.filter(emp => emp.id !== parseInt(req.body.id));
    data.setEmployees([...filteredArray]);
    res.json(data.employees);
}

const getEmployee = (req, res) => {
    const employee = data.employees.find(emp => emp.id === parseInt(req.params.id));
    if (!employee) {
        return res.status(400).json({ "message": `Employee ID ${req.params.id} not found` });
    }
    res.json(employee);
}

module.exports = {
    getAllEmployees,
    createNewEmployee,
    updateEmployee,
    deleteEmployee,
    getEmployee
}
```

### JWT ( Json Web Token)
`$ npm i dotenv jsonwebtoken cookie-parser`
`$ require('crypto').randomBytes (64).toString('hex')`

#### Random Crypto
`> require('crypto').randomBytes(64).toString('hex')`
