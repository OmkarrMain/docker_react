Dockerfile :

FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

Commands :

npm create vite@latest react-app -- --template react
cd react-app
npm install

Docker Commands :

docker build -t react-image .
docker images
docker run -d -p 8081:80 --name react-container react-image
docker ps

Stop :

docker stop react-container
docker rm -f react-container
