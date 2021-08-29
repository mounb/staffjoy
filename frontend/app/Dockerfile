FROM node:12-alpine3.14 as builder
WORKDIR '/build'
COPY app ./app
COPY resources ./resources
COPY third_party ./third_party

WORKDIR '/build/app'
RUN npm set registry https://registry.npm.taobao.org # 注册模块镜像
RUN npm set disturl https://npm.taobao.org/dist # node-gyp 编译依赖的 node 源码镜像
RUN npm set chromedriver_cdnurl http://cdn.npm.taobao.org/dist/chromedriver # chromedriver 二进制包镜像
RUN npm set operadriver_cdnurl http://cdn.npm.taobao.org/dist/operadriver # operadriver 二进制包镜像
RUN npm set phantomjs_cdnurl http://cdn.npm.taobao.org/dist/phantomjs # phantomjs 二进制包镜像
RUN npm set sass_binary_site http://cdn.npm.taobao.org/dist/node-sass # node-sass 二进制包镜像
RUN npm set electron_mirror http://cdn.npm.taobao.org/dist/electron/ # electron 二进制包镜像

RUN npm install
RUN npm rebuild node-sass
RUN npm run build

RUN ls /build/app/dist

FROM nginx
EXPOSE 80
COPY --from=builder /build/app/dist /usr/share/nginx/html


