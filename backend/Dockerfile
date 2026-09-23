
FROM node:22-alpine AS base
WORKDIR /app

# ---- Dépendances 
FROM base AS deps
COPY package.json package-lock.json ./
RUN npm ci

# ---- Dev
FROM deps AS dev
COPY . .
EXPOSE 3001
CMD ["npm", "run", "start:dev"]

# ---- Build
FROM deps AS build
COPY . .
RUN npm run build && npm prune --omit=dev

# ---- Prod 
FROM base AS prod
ENV NODE_ENV=production
COPY --from=build --chown=node:node /app/package.json ./
COPY --from=build --chown=node:node /app/node_modules ./node_modules
COPY --from=build --chown=node:node /app/dist ./dist
USER node
EXPOSE 3001
CMD ["node", "dist/main.js"]
