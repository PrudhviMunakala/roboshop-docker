FROM redhat/ubi9
ENV MONGO_DB_URL=mongodb-dev.ptdevops.online \
    MONGO_DB_NAME=roboshop \
    MONGO_DB_PASSWORD=roboshop123 \
    MONGO_DB_USERNAME=mongodb
LABEL name = "devops" \
      version = "1.0.0" \ 
      description = "This is a nginx image for devops project" \ 
      maintainer = "devops team"
EXPOSE 80
RUN yum install nginx -y
CMD [ "nginx", "-g", "daemon off;" ]
