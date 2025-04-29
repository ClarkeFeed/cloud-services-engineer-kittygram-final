FROM python:3.10

WORKDIR /app
COPY requirements.txt .
RUN apt update && apt install telnet
RUN pip install -r requirements.txt --no-cache-dir
COPY . .
CMD ["gunicorn", "--bind", "0.0.0.0:9000", "kittygram_backend.wsgi"]