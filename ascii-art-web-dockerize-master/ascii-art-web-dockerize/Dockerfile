# Dockerfile References: https://docs.docker.com/engine/reference/builder/
# FROM scratch
# LABEL maintainer="M.a_k & Araya"
# ADD cmd/main /
# ADD ./ui/html/*.html /ui/html/
# ADD ./ui/static/*.css /ui/static/
# ADD ./ui/static/*.png /ui/static/
# ADD shadow.txt /
# ADD standard.txt /
# ADD thinkertoy.txt /
# ADD README.md /
# # ENV API_BOLTDB_PATH='bolt.db'
# # ENV API_HOSTNAME=':8080'

# CMD ["/main"]

# EXPOSE 8080

FROM golang:alpine AS builder
WORKDIR /app
COPY . .
RUN go build -o main cmd/main.go

FROM alpine:3.6
WORKDIR /app
COPY --from=builder /app/main .
COPY --from=builder /app/ui /app/ui
COPY --from=builder /app/internal /app/internal
COPY --from=builder /app/standard.txt /app/standard.txt
CMD ["/app/main"]