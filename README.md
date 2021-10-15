# jenkins-pipeline-tests

Hello World para testar as pipelines do Jenkins.<br>
Subindo jenkins com Docker Compose para testes.

 Volume <b>jenkins_data</b> é criado na pasta <b>/var/lib/docker/volumes</b>.<br>
 Bind mount <b>/data</b> para colocar arqui no container. ($PWD = diretório atual, neste caso diretório do arquivo)

```yml
# docker-compose.yml
version: '3.7'

services:
  jenkins:
    container_name: jenkins-ctnr
    image: jenkins/jenkins:lts
    deploy:
      resources:
        limits:
          cpus: 1.50
          memory: 2048M
        reservations:
          cpus: 1
          memory: 1048M

    privileged: true
    user: root
    ports:
      - 8080:8080
      - 50000:50000
    volumes:
      - jenkins_data:/var/jenkins_home
      - $PWD/data:/jenkins_data
      - /var/run/docker.sock:/var/run/docker.sock

volumes:
  jenkins_data:

```
