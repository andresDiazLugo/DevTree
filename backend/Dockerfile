# ETAPA 1: BUILDER
FROM node:22-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .

RUN npm run build


# ETAPA 2: RUNNER
FROM node:22-alpine AS runner

WORKDIR /app

COPY package*.json ./

RUN npm ci --omit=dev

COPY --from=builder /app/dist ./dist

# Copiar variables de entorno desde el proyecto local
COPY .env .env

EXPOSE 4000

CMD ["npm", "start"]