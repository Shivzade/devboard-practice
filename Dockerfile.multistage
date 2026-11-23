# Stage 1 (Builder Stage ) - Used to build packages and apps
FROM node:24 AS builder

# This will create a folder and make it as PWD
WORKDIR /app

# Copy all the code
COPY . .

# This will install all the packages
RUN npm install --legacy-peer-deps

# This will create a folder call /dist
RUN npm run build  --legacy-peer-deps


#------------ Stage 1 complete --------

#Stage 2 (runner Stage) - Used to run the application from the builder stage
FROM node:24-alpine AS runner

WORKDIR /app

COPY package.json . 

RUN npm install -g vite

COPY --from=builder /app/dist ./dist

CMD ["npm", "run", "preview", "--", "--host", "0.0.0.0", "--port", "4173"] 
