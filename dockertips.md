### Run Swagger Generate Spec inside a docker container
```
docker run --rm -it golang
go get -u github.com/go-swagger/go-swagger/cmd/swagger
git clone https://github.com/pdrum/swagger-automation /app && cd /app
swagger generate spec -o ./swagger.yaml --scan-models
```
