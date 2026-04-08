# ================================
# Stage 1: Builder
# ================================
FROM python:3.9 AS builder

WORKDIR /app

# Copy only requirements first (layer caching benefit)
COPY requirements.txt .

# Install dependencies into a specific folder (not system-wide)
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt

# ================================
# Stage 2: Runtime
# ================================
FROM python:3.9-slim AS runtime

EXPOSE 8080
WORKDIR /app

RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /app

# Copy only installed packages from builder stage
COPY --from=builder /install /usr/local

# Copy only application files needed at runtime
COPY --chown=roboshop:roboshop payment.ini .
COPY *.py .
USER roboshop
CMD ["uwsgi", "--ini", "payment.ini"]

# FROM python:3.9
# EXPOSE 8080
# WORKDIR /app
# COPY payment.ini .
# COPY *.py .
# COPY requirements.txt .
# RUN pip3 install -r requirements.txt
# CMD ["uwsgi", "--ini", "payment.ini"]