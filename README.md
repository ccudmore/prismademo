# How this project was built

## Create the project
1. Create a Postgres Database and create a user that can connect and modify the database and the schema
2. Run the following commands to create and initialize the project
```sh
npx sv create prismademo
cd prismademo
npm i -D @sveltejs/adapter-node
npm install prisma tsx @types/pg --save-dev
npm install @prisma/client @prisma/adapter-pg dotenv pg
npx prisma init --output src/generated/prisma - done to here
```

3 edit vite.config.js and change:
 - import adapter from '@sveltejs/adapter-auto'
 + import adapter from '@sveltejs/adapter-node'

4.  Create .env and edit it to change DATABASE_URL to connect to the database with the configured userid and password. Also create a .env.example with an empty DATABASE_URL value

5.  Edit prisma/schema.prisma and add the test schema

6. Create prisma/seed.ts to create data seed instructions

7.  Edit prisma.config.ts to add seed line

8. Run the following commands to initialize prisma and push the database schema and seed data to the database
```sh
npx prisma generate
npx prisma db push
npx prisma db seed
```

If you're running in a docker image, run the following commands once the container is up:
docker exec -it prismademo npx prisma db push
docker exec -it prismademo npx prisma db seed

9. Create Dockerfile, .gitignore and .dockerignore files

10. Push to GitHub
Craig to do


## Configuring the database
Run the following script on the database to create the user that will be used to connect

```sh
CREATE USER opencupboard WITH PASSWORD 'mypassword';
GRANT ALL PRIVILEGES ON DATABASE opencupboard TO opencupboard;
GRANT ALL PRIVILEGES ON SCHEMA public to opencupboard
```

This an also be done using the Postgres Manager


## Running the project locally
```sh
npm run dev
```

## Building a local Docker image and running it in Docker
```sh
docker build . -t prismademo
docker run -d -p 3000:3000 --name prismademo --env-file .env prismademo
```

## Building a Docker image in GitHub and running it


# Utility functions
- push the updated database schema
- run the prisma browser



## Running the project locally
```sh
docker build . -t prismademo
docker build . -t prismademo
npm run dev
```

# Utility functions
- push the updated database schema
- run the prisma browser

# Setting up the github repo:
1. Create the project in github and get the link
2. Add the following secrets to the repo (Settings > Secrets and variables > Actions > Repository Secrets:
DOCKER_TOKEN:
DOCKER_USERNAME:

```sh
git init
```
Update .gitignore
Add .github/workflows/docker-image.yml
```sh
git add .
git commit -m ‘initial load’
git branch -M main
git remote add origin https://github.com/ccudmore/prismademo.git
git push -u origin main
```

See https://www.prisma.io/docs/guides/deployment/docker
