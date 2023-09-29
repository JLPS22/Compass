# Lab AWS S3
Fazer com que um bucket do Amazon S3 funcione como hospedagem de conteúdo estático.

## Criação de um Bucket:
Nome do bucket: exercicioum.com
![Criando um bucket](../Evidencias/Exercicio_1/Criando_Bucket.png)

## Habilitando hospedagem de site estático:

![Habilitando hospedagem de site estático](../Evidencias/Exercicio_1/Static_Website_Hosting.png)

## Editando as configurações do Bloqueio de acesso público:

![Editando as configurações do Bloqueio de acesso público](../Evidencias/Exercicio_1/Block_Public_Access.png)

## Adicionando política de bucket que torna o conteúdo do bucket publicamente disponível:

![Adicionando política de bucket que torna o conteúdo do bucket publicamente disponível](../Evidencias/Exercicio_1/Bucket_Policy.png)

## Configurando um documento de índice e um documento de erros:
Index.html:
```
<html xmlns="http://www.w3.org/1999/xhtml" >
<head>
    <title>Home Page do meu WebSite - Tutorial de S3</title>
</head>
<body>
  <h1>Bem-vindo ao meu website</h1>
  <p>Agora hospedado em Amazon S3!</p>
  <a href="dados/nomes.csv">Download CSV File</a> 
</body>
</html>
```

![Documento de índice e documento de erros](../Evidencias/Exercicio_1/Objects.png)

## Testando o Endpoint do site:

![Endpoint](../Evidencias/Exercicio_1/Endpoint.png)