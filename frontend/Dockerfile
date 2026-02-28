# Use a lightweight Node image
FROM node:18-alpine

# Set the working directory
WORKDIR /app

# Install the 'serve' package globally
RUN npm install -g serve

# Copy your existing 'dist' folder into the container
COPY dist ./dist

# Expose port 3000
EXPOSE 3000

# Start the server on port 3000
CMD ["serve", "-s", "dist", "-l", "3000"]