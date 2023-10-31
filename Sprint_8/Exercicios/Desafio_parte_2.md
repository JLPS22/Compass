# Desafio - Parte 2
Neste etapa do desafio iremos capturar dados do TMDB via AWS Lambda realizando chamadas de API. Os dados coletados devem ser persistidos em Amazon S3, camada RAW Zone, mantendo o formato da origem (JSON) e, se possível, agrupando-os em arquivos com, no máximo, 100 registros cada.

O objetivo desta etapa é complementar os dados dos Filmes e Series, carregados na Etapa 1, com dados oriundos  TMDB e, opcionalmente, de outra API de sua escolha.

`Transformando e filtrando os arquivos csv para o json e fazendo o upload para o s3.`

**Código:**
```
import pandas as pd
import boto3
import json
import os
from datetime import datetime

s3 = boto3.client('s3', aws_access_key_id='AKIAUZ3U2GVMUG45U3I2',aws_secret_access_key='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')

bucket_name = 'desafiobucket'
file_movies = 'Raw/Local/CSV/Movies/2023/10/19/movies.csv'
file_series = 'Raw/Local/CSV/Series/2023/10/19/series.csv'
aws_raw_zone = 'Raw/'

objFilme = s3.get_object(Bucket=bucket_name, Key=file_movies)
objSerie = s3.get_object(Bucket=bucket_name, Key=file_series)

with objFilme['Body'] as stream:
    filmeR = stream.read()
    
with objSerie['Body'] as stream:
    serieR = stream.read()
    
with open("dadosMovies.csv", "wb") as arq:
    arq.write(filmeR)
    
with open("dadosSeries.csv", "wb") as arq:
    arq.write(serieR)
    
moviesCSV = pd.read_csv("dadosMovies.csv", sep="|")
seriesCSV = pd.read_csv("dadosSeries.csv", sep="|")

movies = moviesCSV.replace(r'\N', 'NULL')
series = seriesCSV.replace(r'\N', 'NULL')

moviesJson = []
seriesJson = []

moviesDrama = movies[movies['genero'] == 'Drama']
seriesDrama = series[series['genero'] == 'Drama']
moviesJson.append(moviesDrama.to_dict(orient='records'))
seriesJson.append(seriesDrama.to_dict(orient='records'))

moviesRomance = movies[movies['genero'] == 'Romance']
seriesRomance = series[series['genero'] == 'Romance']
moviesJson.append(moviesRomance.to_dict(orient = 'records'))
seriesJson.append(seriesRomance.to_dict(orient = 'records'))

moviesDramaRomance = movies[movies['genero'] == 'Drama,Romance']
seriesDramaRomance = series[series['genero'] == 'Drama,Romance']
moviesJson.append(moviesDramaRomance.to_dict(orient='records'))
seriesJson.append(seriesDramaRomance.to_dict(orient='records'))

with open('movies.json', 'w') as arquivo_json:
    json.dump(moviesJson, arquivo_json, indent = 2)
    
with open('series.json', 'w') as arquivos_json:
    json.dump(seriesJson, arquivos_json, indent = 2)
    
arquivos = ['movies.json', 'series.json']
data_processamento = datetime.now().strftime('%Y/%m/%d/')

for arquivo in arquivos:
    
    if 'movies' in arquivo.lower():
        tipo = 'Movies/'
    else:
        tipo = 'Series/'
    
    caminho_destino = os.path.join(aws_raw_zone, 'Local/', 'JSON/', tipo, data_processamento, arquivo)
    s3.upload_file(os.path.join(arquivo), bucket_name, caminho_destino)
```

`Dividindo arquivo movies.json e series.json em outros 50 arquivos json, com cada um contento 100 registros.`

**Código:**
```
import boto3
import json
import os
from datetime import datetime

def loadJson(file, dados):
    with open(file, 'w') as add:
        json.dump(dados, add, indent=2)

def load_s3_Filmes(arquivo, aws_raw_zone):
    
    s3 = boto3.client('s3', aws_access_key_id='AKIAUZ3U2GVMUG45U3I2',aws_secret_access_key='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')
    data_processamento = datetime.now().strftime('%Y/%m/%d/')
    aws_bucket_name = 'desafiobucket'
    
    print(arquivo)
    caminho_destino = os.path.join(aws_raw_zone, 'TMDB/', 'JSON/', 'Movies/', data_processamento, arquivo)
    s3.upload_file(os.path.join(arquivo), aws_bucket_name, caminho_destino)

def load_s3_Series(arquivo, aws_raw_zone):
    s3 = boto3.client('s3', aws_access_key_id='AKIAUZ3U2GVMUG45U3I2',aws_secret_access_key='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')
    data_processamento = datetime.now().strftime('%Y/%m/%d/')
    aws_bucket_name = 'desafiobucket'
    
    print(arquivo)
    caminho_destino = os.path.join(aws_raw_zone, 'TMDB/', 'JSON/', 'Series/', data_processamento, arquivo)
    s3.upload_file(os.path.join(arquivo), aws_bucket_name, caminho_destino)

s3 = boto3.client('s3', aws_access_key_id='AKIAUZ3U2GVMUG45U3I2',aws_secret_access_key='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')

bucket_name = 'desafiobucket'
file_movies_Json = 'Raw/Local/JSON/Movies/2023/10/31/movies.json'
file_series_Json = 'Raw/Local/JSON/Series/2023/10/31/series.json'
aws_raw_zone = 'Raw/'

objFilme = s3.get_object(Bucket=bucket_name, Key=file_movies_Json)
objSerie = s3.get_object(Bucket=bucket_name, Key=file_series_Json)

with objFilme['Body'] as stream:
    filmeR = stream.read()
    
with objSerie['Body'] as stream:
    serieR = stream.read()
    
with open("dadosMovies.json", "wb") as arq:
    arq.write(filmeR)
    
with open("dadosSeries.json", "wb") as arq:
    arq.write(serieR)
    
with open("dadosMovies.json", "r") as movies:
    moviesJson = json.load(movies)
    
with open("dadosSeries.json", "r") as series:
    seriesJson = json.load(series)

filme = []
series = []
cont = 1

for num in range(len(moviesJson)):
    
    for moviesAdd in moviesJson[num]:
        
        if cont <= 15:
        
            if moviesAdd["genero"] == "Drama" and moviesAdd['anoLancamento'] >= 1950:
                filme.append(moviesAdd)
            
            if len(filme) == 100:
                nome = "filme-Drama-"
                nome = nome + str(cont) + '.json'
                loadJson(nome, filme)
                load_s3_Filmes(nome, aws_raw_zone)
                cont = cont + 1
                filme = []
        
        elif cont <= 30:
            if moviesAdd['genero'] == "Romance":
                filme.append(moviesAdd)
            if len(filme) == 100:
                nome = "filme-Romance-"
                nome = nome + str(cont) + '.json'
                loadJson(nome, filme)
                load_s3_Filmes(nome, aws_raw_zone)
                cont = cont + 1
                filme = []
                
        elif cont <= 50:
            if moviesAdd['genero'] == "Drama,Romance" and moviesAdd['anoLancamento'] >= 1950:
                filme.append(moviesAdd)
            if len(filme) == 100:
                nome = "filme-Drama,Romance-"
                nome = nome + str(cont) + '.json'
                loadJson(nome, filme)
                load_s3_Filmes(nome, aws_raw_zone)
                cont = cont + 1
                filme = []
        
        else: break

cont = 1

for num in range(len(seriesJson)):
    
    for seriesAdd in seriesJson[num]:
        
        if cont <= 15:
            if seriesAdd["genero"] == "Drama" and int(seriesAdd['anoLancamento']) >= 2010:
                series.append(seriesAdd)
            
            if len(series) == 100:
                nome = "series-Drama-"
                nome = nome + str(cont) + '.json'
                loadJson(nome, series)
                load_s3_Series(nome, aws_raw_zone)
                cont = cont + 1
                series = []
        
        elif cont <= 30:
            if seriesAdd['genero'] == "Romance" and int(seriesAdd['anoLancamento']) >= 2010:
                series.append(seriesAdd)
            if len(series) == 100:
                nome = "series-Romance-"
                nome = nome + str(cont) + '.json'
                loadJson(nome, series)
                load_s3_Series(nome, aws_raw_zone)
                cont = cont + 1
                series = []
                
        elif cont <= 50:
            if seriesAdd['genero'] == "Drama,Romance" and int(seriesAdd['anoLancamento']) >= 2010:
                series.append(seriesAdd)
            if len(series) == 100:
                nome = "series-Drama,Romance-"
                nome = nome + str(cont) + '.json'
                loadJson(nome, series)
                load_s3_Series(nome, aws_raw_zone)
                cont = cont + 1
                series = []
        
        else: break
```