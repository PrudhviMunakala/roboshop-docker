FROM python:3.9
WORKDIR /app
EXPOSE 8080
COPY payment.ini .
COPY *.py .
COPY requirements.txt .
RUN pip3 install -r requirements.txt
CMD [ "uwsgi", "--ini", "payment.ini" ]
