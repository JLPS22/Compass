# Questão 03
Apresente o ator/atriz com a maior média de faturamento por filme.

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
                resultado[palavra.split('"')[1]] = float(palavra.split(',')[4])
            continue
        
        resultado[(atores.split(',')[0])] = float(atores.split(',')[3])

ator = max(resultado, key=resultado.get)
with open('etapa-3.txt', 'w') as e3:
    e3.write(f'O ator com a maior média de faturamento por filme é o {ator} com $%.2f' % resultado[ator])
```