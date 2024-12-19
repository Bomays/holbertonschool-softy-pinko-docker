FROM ubuntu:latest
WORKDIR /app
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y python3 python3-pip
RUN rm /usr/lib/python*/EXTERNALLY-MANAGED
RUN pip3 install flask
RUN pip3 install flask-cors
COPY api.py /app/
EXPOSE 5252
CMD ["python3", "api.py"]

# Backend terminal cmd
# docker build -f ./back-end/Dockerfile -t softy-pinko-back-end:task3 ./back-end
# docker run -p 5252:5252 -it --rm --name softy-pinko-back-end-task3 softy-pinko-back-end:task3

# Front end terminal cmd
# docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task3 ./front-end
# docker run -p 9000:9000 -it --rm --name softy-pinko-front-end-task3 softy-pinko-front-end:task3