
FROM rust:1.75-slim-bookworm as builder
RUN apt-get update && apt-get install -y libpq-dev pkg-config
WORKDIR /app
COPY . .
RUN cargo install diesel_cli --version 2.1.1 --no-default-features --features postgres --locked
RUN cargo build --release

FROM debian:bookworm-slim
RUN apt-get update && apt-get install -y libpq5 && rm -rf /var/lib/apt/lists/*
WORKDIR /app
COPY --from=builder /app/target/release/login-app-backend ./server
COPY --from=builder /usr/local/cargo/bin/diesel ./diesel
COPY ./migrations ./migrations
EXPOSE 8080
CMD ["./server"]