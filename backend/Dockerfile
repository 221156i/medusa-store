FROM node:20-alpine AS base
WORKDIR /app
ENV NODE_ENV=production
COPY package.json ./
RUN npm install --include=dev
COPY . .
RUN npm run build
EXPOSE 9000
CMD ["sh", "-c", "npx medusa db:migrate && npm start"]
