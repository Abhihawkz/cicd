FROM python:3.11-slim-bookworm

WORKDIR /app

ENV PYTHONUNBUFFERED=1 \
  PYTHONDONTWRITEBYTECODE=1 \
  PIP_NO_CACHE_DIR=1

# Install system dependencies required for pip packages
RUN apt-get update && apt-get install -y \
  build-essential \
  gcc \
  libffi-dev \
  libssl-dev \
  curl \
  && rm -rf /var/lib/apt/lists/*

# Upgrade pip first
RUN pip install --upgrade pip

# Copy dependency list first (for caching)
COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

# Now copy application code
COPY . .

EXPOSE 8000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
