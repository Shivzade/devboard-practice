FROM golang:1.22-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 go build -o devboard-backend .

# Stage 2: Minimal runtime
FROM dhi.io/golang:1-alpine

WORKDIR /app

# Use --chmod=0755 on COPY instead of a separate RUN chmod command
COPY --from=builder --chmod=0755 /app/devboard-backend ./devboard-backend

USER nonroot

EXPOSE 8080

ENTRYPOINT ["./devboard-backend"]

