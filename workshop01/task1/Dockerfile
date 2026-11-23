FROM python:3.9-slim-bookworm

WORKDIR /app

COPY src/public public
COPY src/templates templates
COPY src/main.py . 
COPY src/utils.py . 
COPY src/run.sh .
COPY src/requirements.txt .

RUN pip install --no-cache-dir --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

ENV PORT="3000"
ENV INSTANCE_NAME="workshop-1"
ENV INSTANCE_HASH="12sqb"

EXPOSE ${PORT}/tcp

SHELL ["/bin/sh", "-c"]

ENTRYPOINT python main.py 


