# Questão 02
Apresente a  média de faturamento bruto por ator.

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

with open('etapa-2.txt', 'w') as e2:
    for i in resultado:
        e2.write(f'{i} $%.2f\n' % resultado[i])
```