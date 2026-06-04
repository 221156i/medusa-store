FROM oven/bun:1-alpine AS base

WORKDIR /app

COPY package.json bun.lock ./
RUN bun install --frozen-lockfile

COPY . .

RUN bun run build

FROM oven/bun:1-alpine AS production

WORKDIR /app

ENV NODE_ENV=production

COPY package.json bun.lock ./
RUN bun install --frozen-lockfile --production

COPY --from=base /app/.next ./.next
COPY --from=base /app/next.config.mjs ./

EXPOSE 8000

CMD ["bun", "run", "start"]
