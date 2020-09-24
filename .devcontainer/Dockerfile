FROM node:lts-buster as build

ENV NODE_ENV=development

WORKDIR /cache

COPY package.json yarn.lock ./
RUN YARN_CACHE_FOLDER="$(mktemp -d)" yarn --frozen-lockfile && rm -rf $YARN_CACHE_FOLDER

COPY .env.example ./.env.development

# Warm up the cache
COPY . /cache
RUN yarn run gatsby build

WORKDIR /workspace
VOLUME ["/workspace/node_modules", "/workspace/.cache", "/workspace/public"]
