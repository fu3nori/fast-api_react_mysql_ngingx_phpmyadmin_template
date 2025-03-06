FROM node:18-alpine

WORKDIR /app

# package.json と package-lock.json を先にコピーして npm install
COPY package*.json ./
RUN npm install

# ソースコードをコピー
COPY . /app

EXPOSE 5174

# Vite のデフォルト開発サーバーを起動
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0", "--port", "5174"]
