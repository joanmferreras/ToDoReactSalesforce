# React + Webpack ToDo App In Visualforce

## Unmanaged Package
1. Install the unmanaged package: [Unmanaged package for sandboxes](https://test.salesforce.com/packaging/installPackage.apexp?p0=04t8L0000004j3x) [Unmanaged package for developer orgs](https://login.salesforce.com/packaging/installPackage.apexp?p0=04t8L0000004j3x)
2. Go to: `/apex/todoapp` on your browser to see the app.

## Local Installation
1. Install [Node.js](https://nodejs.org)
2. On your preferred terminal navigate to a directory where you wish to clone the project and `git clone https://github.com/joanmferreras/ToDoReactSalesforce.git`
3. `cd ToDoReactSalesforce`
4. `npm install`

## Install ngrok for localhost tunneling
Install [ngrok](https://ngrok.com). It provides a way to serve/expose your localhost files to the internet even in **https (required by Visualforce)**.  

**This is great for VF development**. Because now, you can develop React Redux (or angular or whatever) locally and directly load the JS from within Visualforce while you are still developing it! So you won't have to  upload the JS to Static Resource every time you make changes to the code!

For example: In your Visualforce,
Instead of point to static resource, you can point to something that looks like below. Notice that `bundle.js` is actually the main app file that's currently being developed on localhost!
 
`<script src="https://f56c-24-8-42-108.ngrok.io/assets/mainMan.js"/>`

**Note: Once you are done with development, simply copy the final mainMan.js from 'assets/mainMan.js' folder in your localhost (see production section) to static resource and update the url above to point to static resource.**

## Development: Local + Visualforce
*You need two terminal windows open*, one for client and the other for ngrok.

1. In terminal 1, run: `dev-server`. This runs the development server(webpack-dev-server) at port 2992.
2. In terminal 2, point ngrok to 2992 by running: `ngrok http 2992 --host-header="localhost:2992"`. You'll see ngrok w/ urls as shown below. Simpy use the **https** one.
![ngrok in terminal](https://i.imgur.com/kM4Xgjv.png)
3. Open up the ToDoApp Visualforce page we installed on the org through the unmanaged package deployment. Update the javascript file's url to `<your ngrok's https url>/assets/mainMan.js`.
4. Uncomment the script tag that will be used for development.
5. Comment out the script tag below with the $Resource reference (this will be used for the final Production .js file)


## Production (Visualforce)

1. Generate the latest React app by running: `npm run build`
2. This file will be created in the `assets` folder
3. Upload the file to static resource
4. Change the URL in your Visualforce to point to the newly uploaded static resource by `<script src="{!URLFOR($Resource.<your static resource name here>)}"/>`


## Learn More
1. [Learn React by Doing](https://reactjs.org/tutorial/tutorial.html)
2. [Learn React through Concepts](https://reactjs.org/docs/hello-world.html)
3. [Learn how to set up a React Project with Webpacks from scratch](https://www.youtube.com/watch?v=WDpxqopXd9U)