# Build container
FROM node:14.2.0 as builder

COPY ./gmg-app /app/gmg-app
COPY ./gmg-client /app/gmg-client
COPY ./gmg-server /app/gmg-server

RUN cd /app/gmg-app && npm install && npm run build \
#    && rm -rf /app/gmg-app/node_modules \
    && cd /app/gmg-client && npm install \
    && cd /app/gmg-server && npm install

# Running container
FROM node:14.2.0-alpine as runtime
WORKDIR /app/gmg-server
COPY --from=builder /app/gmg-client /app/gmg-client
COPY --from=builder /app/gmg-server /app/gmg-server
COPY --from=builder /app/gmg-app/build /app/gmg-server/public
CMD ["npm", "run", "start:release"]
EXPOSE 80:80
