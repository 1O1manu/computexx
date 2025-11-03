# Use a specific Python version that you have pulled locally
FROM python:3.12-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Set the working directory in the container
WORKDIR /code

# Install system dependencies
# --no-install-recommends keeps the image smaller
RUN apt-get update && apt-get install -y --no-install-recommends \
    postgresql-client \
 && rm -rf /var/lib/apt/lists/*

# Copy Python dependencies and install them
COPY requirements.txt /code/
# Use a local wheel cache if available to avoid network access
RUN pip install --no-cache-dir -r requirements.txt

# Copy the application code into the container
COPY . /code/

# Expose port 8000
EXPOSE 8000

# Apply migrations and start the Django server
CMD ["sh", "-c", "python manage.py migrate && python manage.py runserver 0.0.0.0:8000"]

