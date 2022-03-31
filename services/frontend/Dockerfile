FROM node:16-alpine as nuxtBuild

WORKDIR /nuxtBuild

COPY ./ /nuxtBuild

RUN yarn install && yarn run build

###

FROM node:16-alpine

WORKDIR /app

COPY ./package.json /app/package.json
COPY --from=nuxtBuild /nuxtBuild/.output /app/.output

RUN ( \
    echo '#!/bin/sh'; \
    echo 'if [[ "$NODE_ENV" == "development" ]]; then yarn run dev; else node /app/.output/server/index.mjs; fi' \
    ) > /usr/local/bin/nuxt-entrypoint && chmod +x /usr/local/bin/nuxt-entrypoint

ENV HOST=0.0.0.0
ENV PORT=3000

ENTRYPOINT ["nuxt-entrypoint"]