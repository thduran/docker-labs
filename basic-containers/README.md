Lab 1:
# Puxar imagem
docker pull nginx

# Puxa a imagem, já rodando um container nginx em background (-d) alocando porta (-p 8080:80), 
docker container run -d -p 8080:80 --name meu-nginx nginx

Obs. flag -rm encerra container logo após exec

# Listar apenas containers em execução
docker container ls
ou: docker ps

# Lista todos containers
docker container ls -a 

# Ver logs
docker logs meu-nginx

# Entrar no container
docker exec -it meu-nginx /bin/bash
# ou /bin/sh se não tiver bash