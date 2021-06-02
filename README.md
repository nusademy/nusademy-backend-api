# Nusademy Backend API

![](https://github.com/nusademy/Bangkit2021CapstoneProject/raw/main/logo/logo.png)

## Description
This repository contains the source code of the api backend application from nusademy. This application is used to provide a REST API for the Nusademy mobile application. This application uses the open-source headless CMS Strapi. More details about Strapi can be seen at the following link. <https://strapi.io>

## Features
- Login API for users, teachers and schools.
- User API for edit profile users, teachers and schools.
- Request Teaching API
- Reject/Approve Teaching API
- Temporary Teacher Jobs API
- Guest Teacher API
- Classrom API including Subject Class

# Installation
The following are the installation steps both locally and in production.
## System Requireements
Based on the official documentation from Strapi and our implementation, here are the minimum system requirements to run the Backend API from Nusademy
- Node LTS (v12 or V14) Note that odd-number releases of Node will never be supported (e.g. v13, v15).
- NPM v6 or whatever ships with the LTS Node versions
-Typical standard build tools for your OS (the build-essentials package on most Debian-based systems)
- At least 1 CPU core (Highly recommended at least 2)
- At least 2 GB of RAM (Moderately recommended 4)
- Minimum required storage space recommended by your OS or 32 GB of free space
- Database PostgreSQL >= 10

## Local
The following are the steps to run this application locally:
1. Make sure that git, nodejs, npm, and posgreSQL are installed on your system.
1. Clone this repository with the following command.
```bash 
git clone https://github.com/nusademy/nusademy-backend-api.git
```
1. import the provided database structure
1. Configure config/database.js into your local database environment. 
```javascript
module.exports = ({ env }) => ({
  defaultConnection: 'default',
  connections: {
    default: {
      connector: 'bookshelf',
      settings: {
        client: 'postgres',
        host: env('DATABASE_HOST'),
        database: env('DATABASE_NAME'),
        username: env('DATABASE_USERNAME'),
        password: env('DATABASE_PASSWORD'),
      },
      options: {},
    },
  },
});
```
1. Install all of dependecies that needed with following command.
```bash
yarn install
```
1. To run this program in your local just run following command.
```bash
yarn develop
```
1. Wait a few moments for the application to run successfully, open the address http://localhost:1337/ in the browser to access the API.

## Production 
These steps are based on the official documentation from [Strapi](https://strapi.io/documentation/developer-docs/latest/setup-deployment-guides/deployment/hosting-guides/google-app-engine.html)  with minor changes from us. The following are the steps for running this application in production:

1. Make sure you already have a Google Cloud Platform account.
1. Go to Console and open Google Cloud Shell.
1. Create a new bucket to store the Backend API configuration file with the following command, please skip it if you already have a bucket.
```bash
gsutil mb gs://example/
```
1. Create an app.yaml file for the App Engine Backend API configuration. Fill app.yaml with the following configuration (Match the credentials and database to your environment.): 
	```
	runtime: nodejs10

	instance_class: F2

	env_variables:
	  HOST: '0.0.0.0'
	  NODE_ENV: 'production'
	  DATABASE_HOST: '/cloudsql/<instance_identifier>'
	  DATABASE_NAME: 'strapi'
	  DATABASE_USERNAME: 'postgres'
	  DATABASE_PASSWORD: '<password>'

	  beta_settings:
	  cloud_sql_instances: '<instance_identifier>'

	```
1. Copy app.yaml to Storage Bucket with the following command:
```bash
gsutil cp app.yaml gs://example/app.yaml
```
1. Create an App Engine service with the following command
```bash
gcloud app engine create
```
1. Deploy Backend API to App Engine service.
```bash
gcloud app deploy
```

## CI/CD


2. Before setting up CI/CD, first connect Cloud Build with Repository. Cloud Build -> Trigger -> Connect Repository.
2. Create a Trigger for CI/CD, specify the repository, then in the substitution variables enter the following key (cloudbuild.yaml telah kami sediakan pada repository.):   
```bash
_BUCKET  =  example
```
2. Click Save, then Run Trigger.

# END
