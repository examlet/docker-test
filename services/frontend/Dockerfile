FROM node:16-alpine

WORKDIR /app

COPY ./ .

RUN yarn install && yarn run build

RUN ( \
    echo '#!/bin/sh'; \
    echo 'if [[ "$NODE_ENV" == "development" ]]; then yarn run dev; else node /app/.output/server/index.mjs; fi' \
    ) > /usr/local/bin/nuxt-entrypoint && chmod +x /usr/local/bin/nuxt-entrypoint

ENV HOST=0.0.0.0

ENTRYPOINT ["nuxt-entrypoint"]