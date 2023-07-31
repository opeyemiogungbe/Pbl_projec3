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

`vim api.js`

