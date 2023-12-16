# Use an official Python runtime as a parent image
#FROM python:3.8-slim
FROM python:3.10-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Create and set the working directory
WORKDIR /usr/src/app/

# Install system dependencies
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        zlib1g-dev \
        libjpeg-dev \
        gcc \
        musl-dev \
        libpq-dev \
        libffi-dev \
        libcairo2-dev \
        libpango1.0-dev \
        libgdk-pixbuf2.0-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt /usr/src/app/requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copy the Django project code into the container
COPY . /usr/src/app/
CMD celery -A myshop worker -l info
