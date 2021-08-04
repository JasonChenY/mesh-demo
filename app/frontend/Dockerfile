FROM npmjs/npm-docker-baseline:12-alpine AS builder
RUN mkdir /myproj
COPY src  /myproj/src
COPY public /myproj/public
COPY package.json  package-lock.json yarn.lock /myproj/
WORKDIR /myproj
RUN npm install && npm run-script build

FROM ccr.ccs.tencentyun.com/qcloud/nginx:1.9
COPY ./default.conf /etc/nginx/conf.d/ 
COPY --from=builder /myproj/build /usr/share/nginx/html/
EXPOSE 80
ENTRYPOINT nginx -g "daemon off;"

