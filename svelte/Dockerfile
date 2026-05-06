FROM public.ecr.aws/docker/library/node:24.11.1-alpine AS builder
WORKDIR /app
COPY ./package*.json .
RUN npm install
COPY . .
RUN npm run build
# Result : applications will be create in /app/dist path.

FROM public.ecr.aws/nginx/nginx:alpine
COPY ./default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/dist /usr/share/nginx/html
# copy static files which are built on stage1(builder) to nginx's web Root Dir 
