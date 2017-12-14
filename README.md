# Hello with ECS, ALB and ACM

Hello world on containers.

Prepare components.

- Create a key pair
- Create a record set for your domain (e.g. `ecs.example.com`)
- Request a certificate for the domain

Create a cluster.

```sh
brew install amazon-ecs-cli
ecs-cli configure --region ap-northeast-1 --cluster hello
ecs-cli configure profile --access-key *** --secret-key ***

ecs-cli up --capability-iam --keypair hello-keypair
ecs-cli compose service up
```

Create a load balancer.

- Make sure an auto scaling group has been created
- Create an ALB
- Create target groups
  - Host `echo.ecs.example.com` to `ecs:10001`
  - Host `git.ecs.example.com` to `ecs:10002`
- Associate the auto scaling group with target groups
- Create an A record of the wild card domain and map to the ALB

Open URLs.

- https://echo.ecs.example.com should show the request/response
- https://git.ecs.example.com should show the login page

Check the Cloud Watch Logs.
