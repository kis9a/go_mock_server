## Manualy push to ECR (example)

```
docker build -t mock_server_go_docker . --file Dockerfile
export SERVER_PORT=8000
export AWS_ACCOUNT_ID=111111111
docker run --env SERVER_PORT -p $SERVER_PORT:$SERVER_PORT -it $(docker images mock_server_go_docker -q)
docker login -u AWS --password "$(aws ecr get-login-password --region ap-northeast-1 --profile profile)" "https://${AWS_ACCOUNT_ID}.dkr.ecr.ap-northeast-1.amazonaws.com"
docker build -t ${AWS_ACCOUNT_ID}.dkr.ecr.ap-northeast-1.amazonaws.com/dev/mock-server-go-docker:v1.0 .
docker push ${AWS_ACCOUNT_ID}.dkr.ecr.ap-northeast-1.amazonaws.com/dev/mock-server-go-docker:v1.0
```
