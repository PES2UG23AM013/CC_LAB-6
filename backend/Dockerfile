FROM python:3.9-slim

WORKDIR /app

RUN echo "Served by Backend Container" > index.html

CMD ["python3", "-m", "http.server", "8080"]