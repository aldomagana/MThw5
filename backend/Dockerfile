FROM node:18-alpine

WORKDIR /appcopy 

COPY package.json  ./

RUN npm install

COPY . .

RUN mkdir -p /app/data

EXPOSE 5000

CMD ["npm", "start"]
