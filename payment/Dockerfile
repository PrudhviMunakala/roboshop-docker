FROM python:3.9-alpine AS builder

WORKDIR /app

# Install build deps in builder only
RUN apk add --no-cache \
    gcc \
    musl-dev \
    linux-headers \
    libffi-dev \
    openssl-dev \
    pcre-dev

COPY requirements.txt .

# Install to /install prefix
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt

# Verify uwsgi binary exists in builder
RUN ls -la /install/bin/uwsgi

# ================================
# Stage 2: Runtime
# ================================
FROM python:3.9-alpine AS runtime

EXPOSE 8080
WORKDIR /app

# Runtime libs only
RUN apk add --no-cache \
    libffi \
    openssl \
    pcre

# Create user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /app

# Copy installed packages from builder
COPY --from=builder /install /usr/local

# Fix permissions on uwsgi binary
RUN chmod +x /usr/local/bin/uwsgi

# Copy application files
COPY --chown=roboshop:roboshop payment.ini .
COPY --chown=roboshop:roboshop *.py .

USER roboshop

# Use full path to be explicit
CMD ["/usr/local/bin/uwsgi", "--ini", "payment.ini"]



# ================================
# # Stage 1: Builder
# # ================================
# FROM python:3.9 AS builder

# WORKDIR /app

# # Copy only requirements first (layer caching benefit)
# COPY requirements.txt .

# # Install dependencies into a specific folder (not system-wide)
# RUN pip install --no-cache-dir --prefix=/install -r requirements.txt

# # ================================
# # Stage 2: Runtime
# # ================================
# FROM python:3.9-alpine AS runtime

# EXPOSE 8080
# WORKDIR /app

# RUN apk add --no-cache \
#      pcre-dev

# RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
#     chown -R roboshop:roboshop /app

# # Copy only installed packages from builder stage
# COPY --from=builder /install /usr/local

# # Copy only application files needed at runtime
# COPY --chown=roboshop:roboshop payment.ini requirements.txt .
# COPY *.py .
# USER roboshop
# CMD ["uwsgi", "--ini", "payment.ini"]

# FROM python:3.9
# EXPOSE 8080
# WORKDIR /app
# COPY payment.ini .
# COPY *.py .
# COPY requirements.txt .
# RUN pip3 install -r requirements.txt
# CMD ["uwsgi", "--ini", "payment.ini"]