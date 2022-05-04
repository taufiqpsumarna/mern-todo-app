#STAGE 1
FROM node:14 as builder

#Set Wokrdir and Copy Context
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .

#Set ENV
ARG REACT_APP_API_BASE_URL
ENV REACT_APP_API_BASE_URL=$REACT_APP_API_BASE_URL

# Build Package
RUN npm run build

#STAGE 2
FROM nginx:stable-alpine
COPY --from=builder /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
