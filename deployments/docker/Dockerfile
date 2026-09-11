FROM rust:1-bookworm AS builder
WORKDIR /src
COPY . .
RUN cargo build --release -p sdkwork-api-xiangqi-standalone-gateway

FROM debian:bookworm-slim
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates && rm -rf /var/lib/apt/lists/*
WORKDIR /app
COPY --from=builder /src/target/release/sdkwork-api-xiangqi-standalone-gateway /usr/local/bin/sdkwork-api-xiangqi-standalone-gateway
ENV SDKWORK_XIANGQI_APPLICATION_PUBLIC_INGRESS_BIND=0.0.0.0:8098
ENV XIANGQI_API_BIND=0.0.0.0:8098
EXPOSE 8098
CMD ["sdkwork-api-xiangqi-standalone-gateway"]
