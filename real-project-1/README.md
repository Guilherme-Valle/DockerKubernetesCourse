# Aqui foram trabalhados conceitos de volumes e bind

## Como criar um volume nomeado?
`docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback feedback-node:latest`

## Com bind do código:
`docker run -d --rm -p 3000:80 --name feedback-app -v feedback:/app/feedback -v "/home/guilherme/personal/DockerKubernetesCourse/real-project-1:/app" -v /app/node_modules feedback-node:latest`