FROM golang:1.22-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 go build -o devboard-backend .

# Stage 2: Minimal runtimege
FROM dhi.io/golang:1-alpine

WORKDIR /app

# Copy only the compiled binary from the builder stage
COPY --from=builder /app/devboard-backend ./devboard-backend

RUN chmod=0755 ./devboard-backend

USER nonroot

EXPOSE 8080

ENTRYPOINT ["./devboard-backend"]
