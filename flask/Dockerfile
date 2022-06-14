FROM python:3
WORKDIR /usr/src/app
COPY requirements.txt ./
ENV FLASK_APP=app
RUN pip install -r requirements.txt
COPY . .
EXPOSE 80
ENTRYPOINT [ "python3" ]
CMD ["./app.py"]
