FROM node:16-alpine as nuxtBuild

WORKDIR /nuxtBuild

COPY ./ /nuxtBuild

RUN yarn install && yarn run build

###

FROM node:16-alpine

WORKDIR /app

COPY ./package.json /app/package.json
COPY --from=nuxtBuild /nuxtBuild/.output /app/.output

ENV HOST=0.0.0.0
ENV PORT=3000

ENTRYPOINT ["node", ".output/server/index.mjs"]