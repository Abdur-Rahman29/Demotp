# Use an official Python runtime as the base image
FROM python

# Set environment variables to avoid Python buffering
ENV PYTHONUNBUFFERED 1

# Set the working directory inside the container
WORKDIR /app
RUN apt-get update && \
    apt-get install -y build-essential wget && \
    wget https://www.sqlite.org/2023/sqlite-autoconf-3400100.tar.gz && \
    tar -xvf sqlite-autoconf-3400100.tar.gz && \
    cd sqlite-autoconf-3400100 && \
    ./configure && \
    make && \
    make install && \
    cd .. && \
    rm -rf sqlite-autoconf-3400100*

# Ensure the right version of SQLite is installed
RUN sqlite3 --version
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
