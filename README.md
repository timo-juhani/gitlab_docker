# Deploy GitLab on Docker
A small repo that contains Docker Compose file for launching a GitLab server and Runner on Docker.

## Installation

Run with ```docker-compose up -d```

Run the shell script to obtain the initial password:
```
chmod u+x get_initial_password.sh
./get_initial_password.sh
```

Login using the password.

## Add Runner

Self-signed certificates require special attention before you are able to register a Runner:
```
apk update
apk add openssl
openssl s_client -showcerts -connect gitlab-server:443 < /dev/null 2>/dev/null | openssl x509 -outform PEM > /etc/gitlab-runner/certs/gitlab-server.crt
gitlab-runner register --tls-ca-file=/etc/gitlab-runner/certs/gitlab-server.crt
```
