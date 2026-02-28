# Strictly use Python 3.13.3 (slim version for a smaller image size)
FROM python:3.13.3-slim

# Set the working directory inside the container
WORKDIR /app

# Copy requirements first to leverage Docker layer caching
COPY requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the backend source code
COPY . .

# Expose the port your Flask/Python app runs on
EXPOSE 5000

# Command to run the application
CMD ["python", "app.py"]