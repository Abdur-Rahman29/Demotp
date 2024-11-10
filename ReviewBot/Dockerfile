# Use an official Python runtime as the base image
FROM python:3.9-slim

# Set environment variables to avoid Python buffering
ENV PYTHONUNBUFFERED 1

# Set the working directory inside the container
WORKDIR /app

# Copy the requirements file to the container
COPY requirements.txt /app/

# Install dependencies from the requirements file
RUN pip install --no-cache-dir -r requirements.txt

# Copy the entire Django project into the container
COPY . /app/

# Expose port 8000 for Django
EXPOSE 8000

# Start the Django development server (or Gunicorn in production)
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
