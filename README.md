Follow these steps:

Step 1:
#install docker in your server (mine is ubuntu)


sudo apt update
sudo apt install docker.io -y

===============================================================================================
Step 2:
#create a docker file
vim dockerfile



#DockerFile
# Base image with Git and Node.js
FROM node:18 AS build

WORKDIR /app

# Clone the GitHub repo
RUN git clone https://github.com/Gagandeep1611/Chat-Application-Frontend.git .

# Install dependencies using npm ci for clean install
RUN npm ci

# Give permissions to vite binary (just in case)
RUN chmod +x ./node_modules/.bin/vite

# Build the React app
RUN npm run build

# Serve with Nginx
FROM nginx:alpine

# Clean default nginx HTML
RUN rm -rf /usr/share/nginx/html/*

# Copy build output (from dist/) to nginx
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]



==============================================================================================================
Step 3:
#execute below 2 commands only


docker build -t chat-frontend .
docker run -d -p 3000:80 chat-frontend


