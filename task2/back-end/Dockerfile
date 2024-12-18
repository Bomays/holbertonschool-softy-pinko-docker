FROM ubuntu:latest
WORKDIR /app
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y python3 python3-pip
RUN rm /usr/lib/python*/EXTERNALLY-MANAGED
RUN pip3 install flask
COPY api.py /app/
EXPOSE 5252
CMD ["python3", "api.py"]

# docker build -f ./Dockerfile -t softy-pinko:task1 .
# docker run -p 5252:5252 -it --rm --name softy-pinko-task1 softy-pinko:task1
