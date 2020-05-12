# Reaction Commerce

[Reaction](http://reactioncommerce.com) is a headless commerce platform built using Node.js, React, and GraphQL. It plays nicely with npm, Docker and Kubernetes.


# Getting started

Follow the documentation to install Reaction with [Reaction Platform](https://docs.reactioncommerce.com/docs/installation-reaction-platform) for all supported operating systems.

## Start App in Docker Container (Recommended)

```sh
bin/setup # do this after initial clone and after every pull or checkout
docker-compose up -d # starts a MongoDB container and a Reaction API container
docker-compose logs -f api # view Reaction API container logs
```

To stop the API and the MongoDB server, enter `docker-compose down`.

## Start App Without Docker (Not Recommended)

```sh
nvm use
# nvm install if prompted
npm i -g npm
npm install
bin/setup # do this after initial clone and after every pull or checkout
npm run start:dev
```

`CTRL+C` to stop.

## Run Integration Tests in Docker Container (Recommended)

```sh
bin/setup
docker-compose run --rm api npm run test:integration # Test all mutations and queries
docker-compose run --rm api npm run test:integration:query # OR test queries only
docker-compose run --rm api npm run test:integration:mutation # OR test mutations only
docker-compose run --rm api npm run test:integration:file:watch -- <filename> # OR test one file
```

`CTRL+C` to interrupt the test run.

## Run Integration Tests on Local Computer

```sh
docker-compose up -d mongo
npm install
npm run test:integration # Test all mutations and queries
npm run test:integration:query # OR test queries only
npm run test:integration:mutation # OR test mutations only
npm run test:integration:file:watch -- <filename> # OR test one file
```

`CTRL+C` to interrupt the test run.

# Build and Test a Production Image

Build:

```sh
docker build . -t test-api
```

Run:

```sh
dc up -d mongo
docker run --env-file ./.env -p 3000:3000 --network reaction.localhost -it test-api:latest
```

Use an external GraphQL client to test http://localhost:3000/graphql. GraphQL Playground isn't served on GET requests because it's in production mode.

