https://www.go-on-aws.com/lambda-go/lambda_function/simple-lambda/

build
env GOOS=linux GOARCH=amd64 go build -ldflags="-s -w" -o ./dist/main main.go

change file execution permission
chmod +x ./dist/main

package the file in a zip as Lambda upload only accept zipped files
cd ./dist && zip main.zip main && cd ..

deploy
aws lambda update-function-code --function-name  gosimple --zip-file fileb://./dist/main.zip

call the function
aws lambda invoke --function-name gosimple --payload fileb://events/test1.json output/test1.out

{
    "StatusCode": 200,
    "ExecutedVersion": "$LATEST"
}

This is not the answer from the Lambda function, but the answer from the Lambda services, which tells you, that the invocation succeeded.

The output from the Lambda function is in `output/test1.out``
"Hiho does not matter!"
