# Этап сборки
FROM node:18-alpine AS builder

WORKDIR /app

# Копируем зависимости
COPY package.json package-lock.json* ./
RUN npm install

# Копируем исходный код
COPY . .

# Сборка фронтенда
RUN npm run build

# Этап сервера (Nginx)
FROM nginx:1.25-alpine

# Удалим дефолтную страницу nginx
RUN rm -rf /usr/share/nginx/html/*

# Копируем собранные файлы
COPY --from=builder /app/dist /usr/share/nginx/html

# Копируем кастомный конфиг nginx (если есть)
# Убедись, что файл nginx.conf лежит в папке frontend!
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
