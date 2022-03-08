FROM python:3.7-slim
COPY ./ /app
WORKDIR /app
COPY api_yamdb/requirements.txt pwd
RUN pip3 install -r api_yamdb/requirements.txt --no-cache-dir 
CMD ["gunicorn", "api_yamdb.api_yamdb.wsgi", "--bind", "0:5000"] 
