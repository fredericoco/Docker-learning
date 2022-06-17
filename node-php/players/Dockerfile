FROM node
WORKDIR /home/node
COPY package.json package.json
RUN npm install
COPY . .
EXPOSE 80
CMD ["node","server.js"]
