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



Next, i will use the command `npm init` to initialise my new app, so that a new file named package.json will be created. The file will contain information about application and the dependencies that it needs to run.

