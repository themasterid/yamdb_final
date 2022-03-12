FROM python:3.7-slim 
COPY ./ /app
RUN pip3 install -r /app/requirements.txt --no-cache-dir
WORKDIR /app/api_yamdb/
CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000"]
