# Use an Existing docker image as a base
FROM alpine


# Download and install dependency 
RUN apk add --update redis


# Tell image what to do when it starts 
# as a container
CMD [ "redis-server" ]