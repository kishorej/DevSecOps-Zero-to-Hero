#MultiStage Dockerfile
# docker build -t multistage<tagname> .  | docker run -it multistage sh (This will exec into the docker container)
# The below code will reduce the size of the image

#Build Time
FROM node:25 AS builder

WORKDIR /build

COPY package.json ./
RUN npm install

COPY . .

#Run time
# FROM node:25-slim This we are not using as this would be bulky
FROM gcr.io/distroless/nodejs20-debian12
WORKDIR /app
USER appuser
COPY --from=builder /buiild/node_modules ./node_modules
COPY --from=builder /build/app.js ./app.js

EXPOSE 3000
#CMD ["node", "app.js"]
CMD ["app.js"] #No entry point for this distroless image

