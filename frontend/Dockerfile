FROM node:18 as build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

# Build Angular project
RUN npm run build --prod

# Second stage - serve with nginx
FROM nginx:alpine

# Copy Angular build output
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

