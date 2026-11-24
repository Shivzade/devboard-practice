# Pin a specific node version
FROM node:24-alpine

# Run as dedicated non-root user non root.
RUN addgroup -S app && adduser -S -G app app

WORKDIR /app

# Install deps first for better layer caching
COPY package*.json ./
RUN npm ci --legacy-peer-deps

# Copy the source and build the production bundle into /dist
COPY . .
RUN npm run build --legacy-peer-deps

# Hand ownership to the non-root user, then drop previlages
RUN chown -R app:app /app
USER app

# Vite preview serves built bundle to this port
EXPOSE 4173

# 0.0.0.0 so the server is reachable from outside the container. 
CMD ["npm", "run", "preview", "--", "--host", "0.0.0.0", "--port", "4173"]
