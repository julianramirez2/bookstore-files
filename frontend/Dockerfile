FROM node:14 as builder
WORKDIR /home/node/app
COPY package*.json ./

RUN npm install
COPY ./src/ ./src/
COPY ./nginx.conf ./nginx.conf
COPY ./public/ ./public/
COPY ./ssl/ ./ssl/
COPY ./ssl.conf ./ssl.conf

RUN npm run build

# Stage1 
FROM nginx:1.12
WORKDIR /usr/share/nginx/html
COPY --from=builder /home/node/app/build/ ./bookstore/
COPY --from=builder /home/node/app/nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /home/node/app/ssl/ /etc/nginx/ssl/
COPY --from=builder /home/node/app/ssl.conf /etc/nginx/ssl.conf

EXPOSE 80
EXPOSE 43
#multistaging