# Use an Existing docker image as a base
FROM node:alpine

# set working dir
WORKDIR /usr/app

# copy to working dir
COPY ./ ./

# install dependency 

RUN npm install

# Tell image what to do when it starts 
# as a container
CMD [ "npm","start" ]