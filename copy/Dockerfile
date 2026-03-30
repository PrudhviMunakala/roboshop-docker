FROM nginx:1.29.7
RUN rm -rf /usr/share/nginx/html/*
COPY project/ /usr/share/nginx/html/
EXPOSE 80
RUN mkdir images
RUN curl -o images/img1.jpg https://picsum.photos/300/200
RUN curl -o images/img2.jpg https://picsum.photos/301/200
RUN curl -o images/img3.jpg https://picsum.photos/302/200