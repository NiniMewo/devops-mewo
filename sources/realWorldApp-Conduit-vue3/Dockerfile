FROM node:20-slim AS base
ENV PNPM_HOME="/pnpm"
ENV PATH="$PNPM_HOME:$PATH"
WORKDIR /app

COPY . .

RUN corepack enable && pnpm install --frozen-lockfile

FROM base AS dev
EXPOSE 5173
CMD ["pnpm", "dev"]

FROM base AS build
RUN pnpm build

FROM nginx AS prod
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
