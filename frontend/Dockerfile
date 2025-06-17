# Этап сборки
FROM node:18-alpine AS builder

WORKDIR /app

# Копируем весь frontend в рабочую директорию
COPY frontend/ ./

RUN npm install

RUN npm run build

# Этап сервера
FROM nginx:1.25-alpine

# Удалим дефолтную страницу nginx
RUN rm -rf /usr/share/nginx/html/*

# Копируем собранные файлы из билдера
COPY --from=builder /app/dist /usr/share/nginx/html

# Пользовательский конфиг (если нужен SPA fallback)
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
