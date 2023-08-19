# Questão 04
O nome do(s) filme(s) mais frequente(s) e sua respectiva frequência.

## *Resposta:*
```
resultado = []
count = 0
nome = ''
with open('actors.csv','r') as arq:

    dados = arq.read()
    for filme in dados.splitlines():
        if filme.split(',')[0] == 'Actor':
            continue
        if filme[0] == '"':
            for palavra in filme.splitlines():
                resultado.append(palavra.split(',')[5])
            continue
        
        resultado.append(filme.split(',')[4])
        
for item in resultado:
    contagem = 0
    for rep in resultado:
        if rep == item:
            contagem += 1
        
    if contagem > count:
        count = contagem
        nome = item
        
with open('etapa-4.txt', 'w') as e4:
    e4.write(f'O filme que mais frequente é o {nome} com {count}')
```