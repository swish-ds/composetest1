# syntax=docker/dockerfile:1
# Build an image starting with the Python 3.7 image.
FROM python:3.7-alpine

# Set the working directory to /code. Ссылки будут строиться относительно этой папки.
WORKDIR /code
RUN apk add --no-cache gcc musl-dev linux-headers bash

# Copy requirements.txt and install the Python dependencies.
COPY ./files/requirements.txt requirements.txt
RUN pip install -r requirements.txt

# Add metadata to the image to describe that the container is listening on port 5000
EXPOSE 8000

# Copy the current directory (with app.py etc.) . in the project to the workdir . in the image.
COPY ./files/ .

# RUN is an image build step, the state of the container after a RUN command will be committed to the container image. 
RUN touch /code/gerror.log; touch /code/gaccess.log

# CMD is the command the container executes by default when you launch the built image.
CMD gunicorn --bind 0.0.0.0:8000 --workers=1 --log-level=debug --access-logformat '%(h)s %(l)s %(u)s %(t)s "%(r)s" %(s)s %(b)s "%(f)s" "%(a)s"' app:app

# CMD gunicorn --bind 0.0.0.0:8000 --workers=1 --log-level=debug --access-logfile /code/gaccess.log --access-logformat '%(h)s %(l)s %(u)s %(t)s "%(r)s" %(s)s %(b)s "%(f)s" "%(a)s"' --error-logfile /code/gerror.log app:app