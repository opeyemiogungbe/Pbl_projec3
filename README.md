# Projec3 SIMPLE TO-DO APPLICATION ON MERN WEB STACK
i will be implementing MERN Web stack with stands for 

**MongoDB:** A document-based, No-SQL database used to store application data in a form of documents.

**ExpressJS:** A server side Web Application framework for Node.js.

**ReactJS:** A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.

**Node.js:** A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.

![Screenshot 2023-07-31 062952](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/ac97bd9b-53a2-418e-955c-f4e31a469891)

From the image above, we can see we have a user which interacts with the ReactJS UI components at the application front-end in the browser. This frontend is served by the application backend residing in a server, through ExpressJS running on top of NodeJS. While the data change request is sent to the NodeJS based Express server, which grabs necessary data from the MongoDB database, and returns the data to the frontend of the application, which is then presented to the user.

## STEP 1 – BACKEND CONFIGURATION
First i'm going to update and upgrade my ubuntu server running the command:

`sudo atp update`

`sudo apt upgrade`

then i'm going to get the location of Node.js software from Ubuntu repositories. 

`curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -`

then i'm going to install both nodejs and npm. NPM is a package manager for Node like apt for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts running the command:

`sudo apt-get install -y nodejs`

![Screenshot 2023-07-10 052650](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/4f9aa197-81d3-4459-8f3c-167d4fc6503c)

After successful installation of the necessary packages, i'm going to create a Todo directory `mkdir Todo` and` ls` to connfirm and cd into our new Todo directory

![Screenshot 2023-07-10 053113](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/5ed9a1fc-04e9-4b66-9391-505dd7f94b5f)

Next, i will use the command `npm init` to initialise my new app, so that a new file named package.json will be created. The file will contain information about application and the dependencies that it needs to run.

![Screenshot 2023-07-10 060612](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/cb1840bb-04f5-4197-bb0c-b093f5542ad8)

Next, i will Install ExpressJs and create the Routes directory running the following command:

`npm install express` `mkdir Routes `

i'll also be creating index.js file and install dotenv module in there with the command:

`touch index.js` `npm install dotenv`


![Screenshot 2023-07-10 062326](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/f63e8e2a-2099-41a7-819e-8c3bcd3c49e6)

Next i'm going to open the index.js file, put in the code and set the port to run on 5000: 

![Screenshot 2023-07-10 062354](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/16071579-87be-43c6-9ce2-1d9c846a7336)

Now i'll be checking if the configuration in the index.js works fine and run on port 5000:


![Screenshot 2023-07-11 084945](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/f9ede8ab-7423-419a-bae6-c18126a903e8)

Now we need to open port 5000 in EC2 Security Groups on my AWS open my browser and access the server’s Public IP or Public DNS name followed by port 5000:

![Screenshot 2023-07-13 043726](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/ee5e3093-838e-447f-813b-a2951648e06d)


### My To-Do application needs to be able to do 3 things:

1. Create a new task
2. Display list of all tasks
3. Delete a completed task
   
Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.

For each task, i'll need to create routes that will define various endpoints that the To-do app will depend on.

Next i'll be creating a route folder, cd into the folder and create a api.js file in that folder running the following commad:

`mkdir route` `cd route` `touch api.js`

i'll open api.js file with vim text editor and put in the necessary code:

vim api.js

```
const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;
```


Next, from my Todo directory i'm going to install Mongoose which is a Node js package that makes working with mongodb easier. This will help me to create a database model to define the schema. I'll run the command `npm install mongoose`


Next i'm ,going to create a model folder, cd into the new folder and create a file name todo.js running the command below

`mkdir model && cd model && touch todo.js`

i'm going to vi into todo.js and put in the necessary code: 

![Screenshot 2023-07-10 074936](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/1e08b86b-5c14-41b0-b17b-afcd3cf996c9)

Now i'm going to update the file api.js in ‘routes’ directory to make use of the new model. in Routes directory, i opened api.js, delete the code inside with :%d command and paste a new code into it then save and exit.

![Screenshot 2023-07-10 074815](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/20089fa4-c8a0-4e8a-8d9e-02dc8f7e9a3c)

Next i'm going to create a mongodb database and connect it to my dotenv file in my Todo directory

![Screenshot 2023-07-14 103609](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/95612bff-d3b4-4bfd-800b-8cea3fde03d9)

Now i'm going to update the index.js to reflect the use of .env so that Node.js can connect to the database.

```
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/api');
const path = require('path');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

//connect to the database
mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
.then(() => console.log(`Database connected successfully`))
.catch(err => console.log(err));

//since mongoose promise is depreciated, we overide it with node's promise
mongoose.Promise = global.Promise;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use(bodyParser.json());

app.use('/api', routes);

app.use((err, req, res, next) => {
console.log(err);
next();
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
```

Now i'm going to test if my database connected succesfully by running the command `node index.js`

![Screenshot 2023-07-22 054313](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/9bb0427f-19ce-4eda-b766-c62bba07a172)

Now i'm going test my backend code using RESTfull API. i'll be making use of some API development client to test my code, i'll be using Postman to test my API.
i'll be doing both POST request annd GET resquest and the image below shows the result of my testing:



![Screenshot 2023-07-22 060230](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/001a4db1-6c2a-4d8c-9507-b4a377944b5f)



![Screenshot 2023-07-22 060351](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/7dc056f1-f972-4361-b45b-ace8843c0225)


## STEP 2 – FRONTEND CREATION

In this step I'll create the user interface for the Web client (browser) to interact with the application via API. To start out with the frontend of the To-do app intalling react packages in the same root directory as your backend code, which is the Todo directory running the command.

`npx create-react-app client` 

This will create a new folder in my Todo directory called client, where i'll be adding all the react code. Now i'm going to installing nodemon and other necessary packages
```
npm install concurrently --save-dev

npm install nodemon --save-dev
```
In my Todo folder i'll be editing the package.json file with the code below.
```
"scripts": {
"start": "node index.js",
"start-watch": "nodemon index.js",
"dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
},
```

![Screenshot 2023-07-17 071115](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/a9000130-7ee8-436b-ae44-d0b94a593528)

Next, i'll change directory to client `cd client` open the package.json file `vi package.json` and add the key value pair in the package.json file 

`"proxy": "http://localhost:5000"`


Now i'm going to test our connection by running `npm run dev` from the Todo directory to see if the app will open and run on port 3000

![Screenshot 2023-07-17 072514](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/82758d5a-6896-49df-a200-98a966b93001)

from the image above we can see our app is open and run on port 3000 ( note we have to open TCP port 3000 in our Ec2 security group.

### Creating React Components

From my Todo directory, I'll `cd client` and `cd src` from src i'll be creating another folder called component and move into it: 
`mkdir component && cd components` 

Inside ‘components’ directory i'll create three files, Input.js, ListTodo.js and Todo.js with the command:

`touch Input.js ListTodo.js Todo.js`

i'll `vi Input.js` and impute the code below:

```
import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {

state = {
action: ""
}

addTodo = () => {
const task = {action: this.state.action}

    if(task.action && task.action.length > 0){
      axios.post('/api/todos', task)
        .then(res => {
          if(res.data){
            this.props.getTodos();
            this.setState({action: ""})
          }
        })
        .catch(err => console.log(err))
    }else {
      console.log('input field required')
    }

}

handleChange = (e) => {
this.setState({
action: e.target.value
})
}

render() {
let { action } = this.state;
return (
<div>
<input type="text" onChange={this.handleChange} value={action} />
<button onClick={this.addTodo}>add todo</button>
</div>
)
}
}

export default Input
```

Now I'll move into src folder `cd..` and also move into client folder `cd..` i'll install axios `npm install axios` 

Now i'll go back into component directory `cd src/components` and open listTodo.js `vi listTodo.js` and put in thw following code:
```
import React from 'react';

const ListTodo = ({ todos, deleteTodo }) => {

return (
<ul>
{
todos &&
todos.length > 0 ?
(
todos.map(todo => {
return (
<li key={todo._id} onClick={() => deleteTodo(todo._id)}>{todo.action}</li>
)
})
)
:
(
<li>No todo(s) left</li>
)
}
</ul>
)
}

export default ListTodo
```

Then in my Todo.js file i'll put the following code:
```
import React, {Component} from 'react';
import axios from 'axios';

import Input from './Input';
import ListTodo from './ListTodo';

class Todo extends Component {

state = {
todos: []
}

componentDidMount(){
this.getTodos();
}

getTodos = () => {
axios.get('/api/todos')
.then(res => {
if(res.data){
this.setState({
todos: res.data
})
}
})
.catch(err => console.log(err))
}

deleteTodo = (id) => {

    axios.delete(`/api/todos/${id}`)
      .then(res => {
        if(res.data){
          this.getTodos()
        }
      })
      .catch(err => console.log(err))

}

render() {
let { todos } = this.state;

    return(
      <div>
        <h1>My Todo(s)</h1>
        <Input getTodos={this.getTodos}/>
        <ListTodo todos={todos} deleteTodo={this.deleteTodo}/>
      </div>
    )

}
}

export default Todo;
```


**Now i'll be making adjustment to the react code by deleting the logo and adjusting the App.js.**

I'll cd into the src folder and `vi app.js` and put in the code below:
```
import React from 'react';

import Todo from './components/Todo';
import './App.css';

const App = () => {
return (
<div className="App">
<Todo />
</div>
);
}

export default App;
```

Also In the src directory i'll open the App.css `vi App.css` and paste the following code:
```
.App {
text-align: center;
font-size: calc(10px + 2vmin);
width: 60%;
margin-left: auto;
margin-right: auto;
}

input {
height: 40px;
width: 50%;
border: none;
border-bottom: 2px #101113 solid;
background: none;
font-size: 1.5rem;
color: #787a80;
}

input:focus {
outline: none;
}

button {
width: 25%;
height: 45px;
border: none;
margin-left: 10px;
font-size: 25px;
background: #101113;
border-radius: 5px;
color: #787a80;
cursor: pointer;
}

button:focus {
outline: none;
}

ul {
list-style: none;
text-align: left;
padding: 15px;
background: #171a1f;
border-radius: 5px;
}

li {
padding: 15px;
font-size: 1.5rem;
margin-bottom: 15px;
background: #282c34;
border-radius: 5px;
overflow-wrap: break-word;
cursor: pointer;
}

@media only screen and (min-width: 300px) {
.App {
width: 80%;
}

input {
width: 100%
}

button {
width: 100%;
margin-top: 15px;
margin-left: 0;
}
}

@media only screen and (min-width: 640px) {
.App {
width: 60%;
}

input {
width: 50%;
}

button {
width: 30%;
margin-left: 10px;
margin-top: 0;
}
}
```
Also In the src directory i'll open the index.css and put the following code:
```
body {
margin: 0;
padding: 0;
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
"Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
sans-serif;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
box-sizing: border-box;
background-color: #282c34;
color: #787a80;
}

code {
font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
monospace;
}
```
Now i'm going into Todo directory and test my frontend configuration by running the command

`Npm run dev`

if all the code saved successfully without errors my Todo app should be up and running on Tcp port 3000

![Screenshot 2023-07-22 074344](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/747c396b-f223-4205-bc06-dfa641421e67)


![Screenshot 2023-07-22 074414](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/3518cb8d-c804-470d-8d27-3276e0ae09ed)


![Screenshot 2023-07-22 081114](https://github.com/opeyemiogungbe/Pbl_projec3/assets/136735745/14c00bc4-662b-4110-945d-79594c51ca8f)

Yesss!! my Todo app is up and running perfectly.... 

