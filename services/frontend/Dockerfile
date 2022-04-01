FROM node:16-alpine as nuxtBuild

WORKDIR /nuxtBuild

COPY ./ /nuxtBuild

RUN yarn install && yarn run build

###

FROM node:16-alpine

WORKDIR /app

COPY ./package.json /app/package.json
COPY --from=nuxtBuild /nuxtBuild/.output /app/.output

ENV NUXT_PORT=3000
ENV NUXT_HOST=0.0.0.0

ENTRYPOINT ["yarn" ,"start"]