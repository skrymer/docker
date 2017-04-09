
## How to build the image
docker build -t skrymer/rabbitmq-rpi:latest .

## How to run
docker run -P --hostname rabbit1 --name rabbitmq -p 15672:15672 -p 5672:5672 skrymer/rabbitmq-rpi
