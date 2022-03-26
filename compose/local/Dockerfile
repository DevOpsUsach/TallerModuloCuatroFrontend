FROM node:17-alpine3.12 as build

WORKDIR /app

COPY package*.json ./
RUN npm install 

COPY . .

EXPOSE 8000

CMD ["npm", "run", "serve"]