# Use lightweight Python image
FROM python:3.10-slim

# Set working directory
WORKDIR /app

# Install OS packages needed for mysql-connector-python
RUN apt-get update && apt-get install -y gcc default-libmysqlclient-dev && rm -rf /var/lib/apt/lists/*

# Copy files
COPY . /app

# Install dependencies
RUN pip install flask mysql-connector-python

# Expose port
EXPOSE 80

# Run app
CMD ["python", "app.py"]
