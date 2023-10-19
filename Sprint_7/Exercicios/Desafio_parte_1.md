# Desafio - Parte 1
Ingestão Batch: a ingestão dos arquivos CSV em Bucket Amazon S3 RAW Zone. Nesta etapa do desafio deve ser construído um código Python que será executado dentro de um container Docker para carregar os dados locais dos arquivos para a nuvem. Nesse caso utilizaremos, principalmente, as lib boto3 como parte do processo de ingestão via batch para geração de arquivo (CSV).

## Questão 1
Implementar código Python:

- ler os 2 arquivos (filmes e series) no formato CSV inteiros, ou seja, sem filtrar os dados
- utilizar a lib boto3 para carregar os dados para a AWS
- acessar a AWS e grava no S3, no bucket definido com RAW Zone

    - no momento da gravação dos dados deve-se considerar o padrão: `<nome do bucket>` \ `<camada de armazenamento>` \ `<origem do dado>` \ `<formato do dado>` \ `<especificação do dado>` \ `<data de processamento separada por ano\mes\dia>` \ `<arquivo>`

        Por exemplo:

                   S3:\\data-lake-do-fulano\Raw\Local\CSV\Movies\2022\05\02\movies.csv

                   S3:\\data-lake-do-fulano\Raw\Local\CSV\Series\2022\05\02\series.csv

    
### Resposta
Código em Python:

```
import boto3
import os
from datetime import datetime

aws_access_key_id = 'AKIAUZ3U2GVMUG45U3I2'
aws_secret_access_key = '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'
aws_bucket_name = 'desafiobucket'
aws_raw_zone = 'Raw/'

s3 = boto3.client('s3',
                  aws_access_key_id = aws_access_key_id,
                  aws_secret_access_key = aws_secret_access_key)

arquivos = ['movies.csv', 'series.csv']
data_processamento = datetime.now().strftime('%Y/%m/%d/')

for arquivo in arquivos:
    
    if 'movies' in arquivo.lower():
        tipo = 'Movies/'
    else:
        tipo = 'Series/'
    
    caminho_destino = os.path.join(aws_raw_zone, 'Local/', 'CSV/', tipo, data_processamento, arquivo)
    s3.upload_file(os.path.join(arquivo), aws_bucket_name, caminho_destino)
```

## Questão 2
Criar container Docker com um volume para armazenar os arquivos CSV e executar processo Python implementado

### Resposta
Dockerfile:
```
FROM python:3

RUN pip install boto3

COPY movies.csv .
COPY series.csv .
COPY s3.py .

CMD ["python", "s3.py"]
```
Imagem:

![Imagem do container](../Evidencias/img_desafio.png)

## Questão 3
Executar localmente o container docker para realizar a carga dos dados ao S3

### Resposta
Código de execução do container: `docker run -v /arquivos:/arquivos img-desafio`