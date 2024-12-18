FROM ubuntu:latest
WORKDIR /app
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y python3 python3-pip
RUN rm /usr/lib/python*/EXTERNALLY-MANAGED
RUN pip3 install flask
COPY api.py /app/
EXPOSE 5252
CMD ["python3", "api.py"]

# docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task2 ./front-end
# docker run -p 9000:9000 -it --rm --name softy-pinko-front-end-task2 softy-pinko-front-end:task2
