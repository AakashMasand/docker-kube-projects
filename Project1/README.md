# Project 1 - Creating a Production-Grade Workflow with CI and Deployment with AWS

- [X] Create a React Application. Basically, generate a React Application.
- [X] Create a Dockerfile.dev and docker-compose.yml to understand test scenarios for the Docker container.
- [X] Create a Dockerfile for the React App.
- [ ] Setup TravisCI for Continuous Intergration.
- [ ] Setup AWS Elastic Beanstalk.
- [ ] Deploy Application on AWS Elastic Beanstalk.

## Task 1 - Create a React Application. Basically, generate a React Application.

```
npx create-react-app my-app
```

## Task 2 - Create a Dockerfile.dev and understand test scenarios for the Docker container.

```
docker build -t akashmasand/reactapp -f Dockerfile.dev .
```
Build process took 219.5s which is definitely long. Things we can do:

- delete node_modules folder since it will be generated in npm install.
- setup docker volumes for src and public.

### Docker Volumes

```
docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app <image_id>
```
Basically with this command the /app/node_modules will be bookmarked and docker will not map anything against it.

### Docker Compose

Shorthand command is a pain to use and this can basically be made easier using docker-compose.

## Task 3 - Create a Dockerfile for the React App.

### Need for nginx

Basically, we get a Dev Server in our Development environment, however, with the npm run build, the dev server falls away and hence, it is hard to route requests to index.html and main.js.

So, for production, we need a server that responds to web based requests. To solve this, we will use a server named nginx.

### Dockerfile Steps

Unlike what we did in Dockerfile.dev, for our Production Dockerfile, we will divide this into two process - Build and Run.

Build Steps:

- Use node:alpine
- Copy the package.json
- Install Dependencies (technically we only need this step to run the npm run build command successfully)
- Run the npm run build command (Basically, this will generate the files that we need for production)

Run Steps:

- Use nginx
- Copy the results of the npm run build to nginx (/usr/share/nginx/html)
- Start nginx
