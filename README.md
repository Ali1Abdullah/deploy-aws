# deploy-aws
#comment: $1 is file name / $2 is lambda name

.PHONY: build zip deploy

build: 
    GOOS=linux GOARCH=amd64 go build -o ~/environment/build-files/main ~/environment/functions-go/$1.go
zip:
    zip -j ~/environment/zip-files/main.zip ~/environment/build-files/main
deploy: 
    aws lambda update-function-code --function-name $2 --zip-file fileb://~/environment/zip-files/main.zip


