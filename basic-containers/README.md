## Lab 1:

Puxar imagem
```bash
docker pull nginx
```

Puxa a imagem, já rodando um container nginx em background (-d) alocando porta (-p 8080:80)
```bash 
docker container run -d -p 8080:80 --name meu-nginx nginx
```
Obs. flag -rm encerra container logo após exec

Listar apenas containers em execução
```bash
docker container ls
```

Lista todos containers
```bash
docker container ls -a 
```

Ver logs
```bash
docker logs meu-nginx
```

Entrar no container
```bash
docker exec -it meu-nginx /bin/bash
```