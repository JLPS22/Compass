# Questão 01
Apresente o ator/atriz com maior número de filmes e a respectiva quantidade.

## *Resposta:*
```
resultado = {}
with open('actors.csv','r') as arq:

    dados = arq.read()
    for atores in dados.splitlines():
        if atores.split(',')[0] == 'Actor':
            continue
        if atores[0] == '"':
            for palavra in atores.splitlines():
                resultado[palavra.split('"')[1]] = int(palavra.split(',')[3])
            continue
        
        resultado[(atores.split(',')[0])] = int(atores.split(',')[2])
 
ator = max(resultado, key=resultado.get)   
with open('etapa-1.txt', 'w') as e1:
    e1.write(f'O ator com mais filmes é o {ator}\nCom a quantidade de {resultado[ator]} filmes.')
```