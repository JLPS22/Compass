# Q1
Construa uma imagem a partir de um arquivo de instruções (Dockerfile) que execute o código carguru.py. Após, execute um container a partir da imagem criada.

Registre aqui o conteúdo de seu arquivo Dockerfile e o comando utilizado para execução do container.

## *Resposta:*
**Conteúdo do arquivo Dockerfile:**
```
FROM python:3


WORKDIR /app


COPY carguru.py .


CMD ["python", "carguru.py"]
```

**Comandos utilizados:**

Usei o comando ( ```docker build .``` ) para criar a imagem

Depois usei o ( ```docker image ls``` ) para listar as imagens e pegar o código dela

E por fim usei o ( ```docker run <código_da_imagem>``` ) para executa a imagem