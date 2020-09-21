FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx

# This is how you expose a port in a dockerfile
# Cool
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# This is how you copy stuff from previous images
# Notice that because we said "Workdir /app", all our stuff that we want to copy
# will be under the app folder. The npm install and npm run build commands
# will put everything in a build folder that we can just copy over to 
# usr/share/nginx/html, which is the default location nginx looks for files to host
COPY --from=builder /app/build /usr/share/nginx/html
