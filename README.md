# NgJsonServerMock

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 10.0.3.
The Mock Data for applications was was configured with JSON Server

## API mock setup of the application
### Step 1: Initial setup
Assuming that NodeJS, npm & angular-cli is already installed on your machine, please run the following command to create a new Angular project:

### Step 2: Download libraries as below,
`npm install json-server — save-dev` : Install json server

### Step 3: Running JSON Server
Add this to package.json script - “mock:server”: “json-server — watch mocks/data.json”
Now we can run json-server using following command: `npm run mock:server`
Visit http://localhost:3000 to verify if json-server is working fine. 

### Step 4: Setting up proxies for Angular application

We have json-server running at localhost:3000 serving all the required api’s. Now, we need to configure our Angular application to redirect the api calls from 4200(default) to 3000. Our goal is to get valid response for localhost:4200/people. Create a proxy.conf.json file in the root folder and add following script to package.json: “start:proxy”: “ng serve — proxy-config proxy.conf.json”
Add the configuration in proxy.conf.json file

### Step 5: Run angular application
Open a new terminal and run following command to start Angular application using the proxy configurations: `npm run start:proxy`

Visit http://localhost:4200/people and verify if the response data is same as http:localhost:3000/people.

### Step 6: Use concurrently to run both the servers together

Opening two terminals and running two commands is not a good idea for everyday development. Kill any servers which are running. We can use concurrently to overcome this issue. Install concurrently as a dev dependency:
npm install concurrently --save-dev

Add following script to the package.json file:
“start:proxy:mock:server”: “concurrently — kill-others \”npm run mock:server\” \”npm run start:proxy\””

Run the script to start the json server following by Angular application
`npm run start:proxy:mock:server`

### Step 7: Multiple api calls and dataset

Create a new folder “data” inside “mocks” folder and add all mocks

### Step 8: Generate data.json

Install node module “json-concat” in dev dependencies: npm install json-concat — save-dev
Create “concat-json.js” in “mocks” folder. Check the code for more details
Modify package json to generate data.json: “concat:mocks”: “node \”./mocks/concat-json.js\””

### Step 9: Update proxy for multiple file configuration
Modify proxy.config.json: Check the code for more details

### Step 10 Run application
Run the server using: `npm run start:proxy:mock:server`

## Verify the API endpoints
- http://localhost:4200/starwars/people
- http://localhost:4200/starwars/universe/planets
- http://localhost:4200/starwars/universe/transport/starships


## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).
