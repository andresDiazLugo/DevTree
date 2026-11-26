
FROM node:22-alpine AS builder

WORKDIR /app

RUN corepack enable

COPY package.json pnpm-lock.yaml ./

RUN pnpm install --frozen-lockfile

COPY . .

# Copiamos explícitamente el archivo de variables
COPY .env.local .env.local

# Vite lee automáticamente las variables
RUN pnpm build

FROM caddy:alpine AS runner

COPY --from=builder /app/dist /usr/share/caddy

EXPOSE 80

CMD ["caddy", "file-server", "--root", "/usr/share/caddy", "--listen", ":80"]
