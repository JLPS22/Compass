# E7
Dada a seguinte lista:

a = [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

Faça um programa que gere uma nova lista contendo apenas números ímpares.

## *Resposta:*
```
a = [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
b = []

for i in a:
    if i % 2 != 0:
        b.append(i)
    else: continue
    
print(b)
```

![E7](../../Evidencias/Python_1/Exercicio_7.png)