FROM python:3.10-slim-buster
#inside container make a new folder
WORKDIR /backend-flask
#outside container->inside container
#copy libraries needed to run app in the container
COPY requirements.txt requirements.txt
#inside container
#install python libraries used for the app
RUN pip3 install -r requirements.txt
#. means everything in the current directory
#first . means /backend-flask outside container
#second . means /backend-flask inside container
COPY . .
#set environment variable
#inside container
ENV FLASK_ENV=development

EXPOSE ${PORT}
#python -m flask run --host=0.0.0.0 --port=4567
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]