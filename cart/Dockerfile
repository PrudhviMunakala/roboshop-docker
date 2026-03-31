FROM node:20
WORKDIR /app
COPY package.json .
COPY *.js .
RUN npm install
ENV REDIS_HOST="redis" \
    CATALOGUE_PORT="8080" \
    CATALOGUE_HOST="catalogue" 
CMD [ "node", "server.js" ]
