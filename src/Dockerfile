# Build Phase
FROM node:12.4 as builder
WORKDIR /app
COPY /src/gmg-app ./gmg-app
COPY /src/gmg-client ./gmg-client
COPY /src/gmg-server ./gmg-server
COPY /src/build.sh .
RUN apt-get update && \
    apt-get install dos2unix && \
    dos2unix ./build.sh && \
    /bin/bash ./build.sh

# Run Phase
FROM node:8.9.1 as runtime
COPY --from=builder /app/gmg-client /app/gmg-client
COPY --from=builder /app/gmg-server /app/gmg-server
COPY --from=builder /app/gmg-app/build /app/gmg-server/public
WORKDIR /app/gmg-server
CMD ["npm", "run", "start:release"]
EXPOSE 8000:80