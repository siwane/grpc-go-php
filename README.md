
# Install 

## Prepare PHP client

### Install dependencies
```shell script
cd client/ && composer install
```

## Generate php protobuf definition

From root directory
```shell script
GRPC_PHP_PLUGIN_PATH=$(PATH_OF_GRPC_PLUGIN)/bins/opt/grpc_php_plugin
protoc --proto_path=.  \
   --php_out=client/lib \
   --grpc_out=client/lib \
   --plugin=protoc-gen-grpc=$GRPC_PHP_PLUGIN_PATH \
   ./client/service.proto
```
   
## Create GO server

```shell script
cd server/

go run main.go
```
# Run

Run go server that accept grpc connection

`Note that this server needs to be ran before client`

```shell script
go run main.go
```

Run php client

`Note that this client include a timer to calculate time spent on request`

```shell script
php client/greeter_client.php $number_of_outcoming_request
```

# Example of output

```shell script
$ php client/greeter_client.php 1
[...]
This process used 9 ms for its computations
It spent 3 ms in system calls

$ php client/greeter_client.php 10
[...]
This process used 11 ms for its computations
It spent 4 ms in system calls
```
