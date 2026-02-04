#MultiStage Dockerfile
# docker build -t multistage<tagname> .
# This will reduce the size of the image

FROM node:25 AS builder

WORKDIR /build

COPY package.json ./
RUN npm install

COPY . .

FROM node:25-slim
WORKDIR /app
USER appuser
COPY --from=builder /buiild/node_modules ./node_modules
COPY --from=builder /build/app.js ./app.js

EXPOSE 3000
CMD ["node", "app.js"]
