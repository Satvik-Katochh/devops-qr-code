FROM node:18-alpine AS base

# Set the working directory inside the container
WORKDIR /app

# Copy package manager lock files (yarn.lock, package-lock.json, or pnpm-lock.yaml)
COPY package.json yarn.lock* package-lock.json* pnpm-lock.yaml* ./

# Install dependencies based on the lock file present
RUN \
    if [ -f yarn.lock ]; then \
        yarn --frozen-lockfile; \
    elif [ -f package-lock.json ]; then \
        npm ci; \
    elif [ -f pnpm-lock.yaml ]; then \
        corepack enable pnpm && pnpm install --frozen-lockfile; \
    else \
        echo "No lock file found." && exit 1; \
    fi

# Copy the rest of the application files into the container
COPY . .


RUN npm run build

EXPOSE 3000

CMD ["npm", "start"]

