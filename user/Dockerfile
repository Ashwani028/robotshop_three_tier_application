FROM node:18-alpine
ENV INSTANA_AUTO_PROFILE true

WORKDIR /opt/server
COPY . .
RUN npm install 
EXPOSE 8080

CMD ["node", "server.js"]


