FROM redhat/ubi9
LABEL name = "devops" \
      version = "1.0" \ 
      description = "This is a nginx image for devops project" \ 
      maintainer = "devops team"
RUN echo "Hi I'm $name community image for $description and my version is $version"
RUN yum install nginx -y
CMD [ "nginx", "-g", "daemon off;" ]
