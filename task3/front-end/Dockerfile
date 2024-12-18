FROM nginx:latest
COPY softy-pinko-front-end /var/www/html/softy-pinko-front-end
COPY softy-pinko-front-end.conf /etc/nginx/conf.d/default.conf
EXPOSE 9000
CMD ["nginx", "-g", "daemon off;"]

# 'daemon off' with (Global directive '-g')> change default background nginx process 
# to foreground process so it remains active and do not stop just after starting"

# docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task2 ./front-end
# docker run -p 9000:9000 -it --rm --name softy-pinko-front-end-task2 softy-pinko-front-end:task2
