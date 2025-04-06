Follow these steps:

Step 1:
#install docker in your server (mine is ubuntu)


sudo apt update
sudo apt install docker.io -y


Step 2:
#clone this git repo


Step 3:
#execute below 2 commands only


docker build -t chat-frontend .
docker run -d -p 3000:80 chat-frontend
