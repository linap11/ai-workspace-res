FROM python:3.13-slim

# -----------------------
# System environment
# -----------------------
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PYTHONPATH=/app/src

# IMPORTANT: canonical runtime root
WORKDIR /app

# -----------------------
# System dependencies
# -----------------------
RUN apt-get update && apt-get install -y \
    build-essential curl git \
    && rm -rf /var/lib/apt/lists/*

# -----------------------
# Install Python deps
# -----------------------
COPY requirements.txt /app/requirements.txt

RUN pip install --no-cache-dir -r /app/requirements.txt

# -----------------------
# Copy application / full source (overridden by volume in compose), Note we donot copy .env
# -----------------------
COPY src /app/src

# -----------------------
# Expose API
# -----------------------
EXPOSE 8000

# -----------------------
# Start server
# -----------------------
CMD ["uvicorn", "ai_workspace.api.main:app", "--host", "0.0.0.0", "--port", "8000"]

