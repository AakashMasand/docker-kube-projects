# Project 1 - Creating a Production-Grade Workflow with CI and Deployment with AWS
- [X] Create a React Application. Basically, generate a React Application.
- [ ] Create a Dockerfile.dev and understand test scenarios for the Docker container.
- [ ] Create a Dockerfile for the React App.
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
``
Basically with this command the /app/node_modules will be bookmarked and docker will not map anything against it.