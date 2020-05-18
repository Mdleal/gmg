# Build Phase
FROM node:lts-stretch as builder
#RUN apt-get update

RUN mkdir /app
WORKDIR /app
COPY /src/gmg-app /app/gmg-app
COPY /src/gmg-client /app/gmg-client
COPY /src/gmg-server /app/gmg-server
COPY /src/build.sh /app
RUN /bin/bash /app/build.sh

# Run Phase
FROM node:lts-stretch as runtime
COPY --from=builder /app/gmg-client /app/gmg-client
COPY --from=builder /app/gmg-server /app/gmg-server
WORKDIR /app/gmg-server
CMD ["npm", "run", "start:release"]
EXPOSE 80:80
