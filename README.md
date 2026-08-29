# Containerized Node.js and MySQL CI/CD Lab

A hands-on DevOps learning project that combines a Node.js Express application with Docker, Docker Compose, MySQL, automated testing, Jenkins pipeline examples, and Vagrant.

## Background

This repository explores how a small web application moves through the development and delivery lifecycle:

- Run a basic Express service locally
- Connect an application to a database through environment variables
- Package the application as a Docker image
- Run the application and database together with Docker Compose
- Execute tests in a CI pipeline
- Build and publish a versioned container image
- Create a repeatable virtual-machine environment with Vagrant

The repository is preserved as a historical learning lab. It uses legacy runtimes, images, Compose syntax, and sample configuration that must be modernized before reuse.

## Application Modes

### Basic Express Service

`index.js` starts an Express server on port `3000` and returns a `Hello World!` response from the root route.

### MySQL Visitor Counter

`index-db.js` demonstrates application-to-database connectivity:

1. Reads MySQL connection details from environment variables.
2. Connects to the configured database.
3. Creates a `visits` table if it does not exist.
4. Inserts a timestamp for each request.
5. Returns the generated visitor number.

Docker Compose starts this version of the application and links it to a MySQL container.

## Architecture

```text
Browser
   |
   v
Node.js / Express container :3000
   |
   v
MySQL container :3306
```

The web container receives its database name, username, password, and host through environment variables.

## Technologies

- JavaScript and Node.js
- Express
- MySQL
- Docker
- Docker Compose
- Jenkins
- Mocha
- Vagrant
- Git

## Repository Structure

```text
.
├── Dockerfile
├── docker-compose.yml
├── index.js
├── index-db.js
├── package.json
├── package-lock.json
├── test
│   └── test.js
└── misc
    ├── Jenkinsfile
    ├── Jenkinsfile.v2
    └── Vagrantfile
```

- `Dockerfile`: Packages the Node.js application into a container.
- `docker-compose.yml`: Defines the web and MySQL services.
- `index.js`: Basic Express application.
- `index-db.js`: Express application with MySQL-backed visit tracking.
- `test/test.js`: Introductory Mocha test.
- `misc/Jenkinsfile`: Jenkins stages for checkout, testing, image creation, and image publishing.
- `misc/Jenkinsfile.v2`: Extended example that runs tests inside containers and starts a database test container.
- `misc/Vagrantfile`: Defines an Ubuntu virtual machine for a repeatable lab environment.

## Skills Demonstrated

- Containerizing a Node.js application
- Coordinating application and database services
- Supplying configuration through environment variables
- Writing and running an automated test
- Defining Jenkins CI/CD stages
- Testing inside disposable containers
- Tagging images with a source-control commit identifier
- Creating repeatable development infrastructure with Vagrant
- Troubleshooting dependencies across application, container, and database layers

## Historical Jenkins Workflow

The Jenkins examples illustrate the following sequence:

1. Check out the repository.
2. record the short Git commit identifier.
3. Install development dependencies.
4. Run the test suite.
5. Optionally start MySQL and run tests in a linked Node.js container.
6. Build a Docker image tagged with the commit identifier.
7. Authenticate to a container registry and push the image.

The image name and credential identifiers in these files are historical examples and must be replaced with values owned by the person deploying the project.

## Security and Modernization Notes

Do not deploy this repository unchanged.

- Node.js 4.6 is end-of-life and must be replaced with a supported release.
- The historical MySQL image and legacy Docker linking should be replaced.
- The Compose file contains sample database credentials. Use a local untracked environment file or a secrets manager instead.
- Do not expose MySQL port `3306` publicly unless there is a specific secured requirement.
- Pin and update dependencies, then review vulnerability reports.
- Run the application as a non-root container user.
- Add health checks, structured logging, and graceful error handling.
- Replace broad registry credentials with scoped credentials.
- Expand the current introductory test into application and database integration tests.
- Review all images and pipeline plugins before executing the historical configuration.

## Running the Basic Application

Because the committed runtime is outdated, use a supported Node.js version and update dependencies before running the project.

For local inspection:

```bash
npm install
npm test
npm start
```

The basic application listens at:

```text
http://localhost:3000
```

## Portfolio Context

This project demonstrates practical exposure to application containerization, multi-container environments, CI/CD pipeline stages, database connectivity, automated testing, and reproducible infrastructure. Its value is in showing the complete delivery workflow and the ability to identify what must change before a historical lab can meet modern production and security standards.
