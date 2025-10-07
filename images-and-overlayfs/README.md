## 🔬 Lab 1: Verificando imagens

1. Obter imagens

```bash
docker pull ubuntu:20.04
docker pull nginx:latest
```

2. Histórico de camadas

```bash
docker history ubuntu:20.04
docker history nginx
```

Detalhando imagem
```bash
docker inspect nginx
```

Comparação de Imagens

| Imagem | N° de Camadas | Tamanho | Observação |
| :--- | :--- | :--- | :--- |
| ubuntu:20.04 | 6 | 72.8MB | Imagem base |
| nginx | 17 | 192MB | Imagem completa |
| nginx:alpine | 19 | 52.5MB | distro Alpine, + enxuta, ideal para produção |

---

## 🧪 Lab 2: Docker Commit - criando imagem

⚠️ Apenas Dockerfile é recomendado; docker commit ajuda a entender camadas.

Subindo container ubuntu
```bash
docker run -it --name ubuntu-commit ubuntu:20.04 bash
```

Dentro do contêiner:
```bash
apt update && apt install -y curl
exit
```

Commit para nova imagem:
```bash
docker commit ubuntu-commit thiagoduran/ubuntu-curl:v1
```

Verificar nova imagem
```bash
docker image ls
docker image history thiagoduran/ubuntu-curl:v1
```

O tamanho da nova imagem dobrou (147MB), pois uma nova camada foi adicionada.


❌ Por que evitar docker commit?

Commit não é ideal para produção pois, ao contrário do Dockerfile, ele não documenta a construção da imagem, gera imagens inseguras e desnecessariamente maiores, pois até cache é copiado do container pra formar a imagem.

---

## 🖼️ Lab 3: Visualizando criação de camadas

Conteiner alpine
```bash
docker run -it --name cow-test alpine sh
```

Executa um contêiner Alpine
```bash
docker run -it --name cow-test alpine sh
```

Dentro do container:
```bash
echo "hello" > /tmp/arquivo.txt
exit
```

Commit
```bash
docker commit cow-test thiagoduran/alpine-cow:v1
```

Container baseado na nova imagem:
```bash
docker run -it thiagoduran/alpine-cow:v1 sh
cat /tmp/arquivo.txt
```

"Hello" foi mostrado, ou seja, a modificação virou nova camada.