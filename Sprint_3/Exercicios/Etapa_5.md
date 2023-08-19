# Questão 05
A lista dos atores ordenada pelo faturamento bruto total, em ordem decrescente.

## *Resposta:*
```
resultado = {}
pos = 1
with open('actors.csv','r') as arq:

    dados = arq.read()
    for atores in dados.splitlines():
        if atores.split(',')[0] == 'Actor':
            continue
        if atores[0] == '"':
            for palavra in atores.splitlines():
                resultado[palavra.split('"')[1]] = float(palavra.split(',')[2])
            continue
        
        resultado[(atores.split(',')[0])] = float(atores.split(',')[1])

with open('etapa-5.txt', 'w') as e5:
    for i in sorted(resultado, key=resultado.get, reverse=True):
        e5.write(f'{pos}) {i} : $%.2f\n' % resultado[i])
        pos += 1
```