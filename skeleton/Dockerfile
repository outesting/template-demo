FROM node:16 as build-deps
WORKDIR /usr/src/app
COPY package.json ./
RUN yarn
COPY . ./
RUN yarn build

FROM nginx:1.21-alpine
RUN rm -rf /usr/share/nginx/html
COPY --from=build-deps /usr/src/app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
