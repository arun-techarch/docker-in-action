# Use official Python slim image
FROM python:latest

# Create a working directory
WORKDIR /app

# Install dependencies first (layer caching)
COPY requirements.txt .

RUN pip install --upgrade pip && \
    pip install -r requirements.txt

# Copy project files
COPY . .

# Expose the port Uvicorn will run on
EXPOSE 8000

# Start python script
CMD ["python", "app/main.py"]