FROM arm32v7/node:8.11.3

USER root
WORKDIR /var/www/
RUN mkdir -p ghost && \
    apt-get update && \
    apt-get -qy install wget unzip && \
    wget https://github.com/TryGhost/Ghost/releases/download/1.25.2/Ghost-1.25.2.zip -o ghost.zip && \
    unzip ghost.zip -d ghost && \
    rm ghost.zip && \
    apt-get -y remove wget unzip && \
    rm -rf /var/lib/apt/lists/* && \
    useradd ghost -m -G www-data -s /bin/bash && \
    chown ghost:www-data . && \
    chown ghost:www-data ghost && \
    chown ghost:www-data -R ghost/* && \
    npm install -g pm2

USER ghost
WORKDIR /var/www/ghost
RUN /bin/bash -c "time (npm install sqlite3)"
RUN npm install

EXPOSE 2368
EXPOSE 2369
RUN ls && pwd

ENV NODE_ENV production

RUN sed -e s/127.0.0.1/0.0.0.0/g ./config.example.js > ./config.js

VOLUME ["/var/www/ghost/content/apps"]
VOLUME ["/var/www/ghost/content/data"]
VOLUME ["/var/www/ghost/content/images"]

CMD ["pm2", "start", "index.js", "--name", "blog", "--no-daemon"]
