FROM python:3.7-slim
WORKDIR /app
COPY api_yamdb/requirements.txt /app
RUN pip3 install -r /app/requirements.txt --no-cache-dir 
COPY api_yamdb/ /app
WORKDIR /app
CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:5000"]
