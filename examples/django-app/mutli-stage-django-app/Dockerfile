# Stage 1: Builder
FROM python:3.14-slim AS builder

WORKDIR /app

COPY requirements.txt /app/
COPY devops /app

# install dependencies in a seperate folder
RUN pip install --no-cache-dir --target=/python-packages -r /app/requirements.txt

# Stage 2: Runtime
FROM gcr.io/distroless/python3

WORKDIR /app
ENV PYTHONPATH=/python-packages

# Copy python packages
COPY --from=builder /python-packages /python-packages

# Copy application code
COPY --from=builder /app /app

EXPOSE 8000

CMD ["manage.py", "runserver", "0.0.0.0:8000"]
