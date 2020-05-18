# Build Phase
FROM node:lts-stretch as builder
RUN apt-get update

WORKDIR /app
COPY /srv/gmg-app ./gmg-app
COPY /srv/gmg-client ./gmg-client
COPY /srv/gmg-server /gmg-server
COPY /srv/build.sh .
RUN /bin/bash ./build.sh

# Run Phase
FROM node:lts-stretch as runtime
COPY --from=builder /app/gmg-client /app/gmg-client
COPY --from=builder /app/gmg-server /app/gmg-server
WORKDIR /app/gmg-server
CMD ["npm", "run", "start:release"]
EXPOSE 80:80
