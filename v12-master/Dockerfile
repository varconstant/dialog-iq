# FROM botpress/server:latest
# CMD ["./bp", "&" ,"./duckling"]

FROM --platform=linux/amd64 node:12.22.10

WORKDIR /app

COPY . .
RUN echo $(node -v)
# RUN yarn cache clean
#RUN npm cache clean --force && yarn cache clean && yarn config delete proxy && yarn config delete https-proxy && yarn config delete registry
RUN yarn install --network-timeout 1000000
RUN yarn
RUN yarn build
RUN if [ -f /app/custom-build/studio ]; then \
        echo "File exists, copying..."; \
        cp /app/custom-build/studio /app/packages/bp/dist/bin/studio; \
    else \
        echo "File does not exist"; \
    fi
EXPOSE 3000

ENTRYPOINT [ "yarn", "start"]