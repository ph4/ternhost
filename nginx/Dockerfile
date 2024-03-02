# vite build
FROM node:lts-alpine as build-stage
WORKDIR /app/
COPY ./frontend/package*.json /app/
RUN npm cache verify
RUN npm install
COPY ./frontend /app/
RUN npm run build

# prod
FROM nginx:alpine as production-stage
COPY ./nginx/prod.conf /etc/nginx/nginx.conf
# COPY backend/static /usr/src/app/static/
COPY --from=build-stage /app/dist /dist
EXPOSE 8884
CMD ["nginx", "-g", "daemon off;"]
