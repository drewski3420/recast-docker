FROM python:3.10-slim-bullseye

WORKDIR /app

#Install dependencies
COPY . . 

RUN pip install --upgrade pip
RUN pip3 install -r requirements.txt

##Run it
ENTRYPOINT ["python", "manage.py", "runserver", "0.0.0.0:8000"]
