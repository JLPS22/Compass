# E4
Escreva um código Python para imprimir todos os números primos entre 1 até 100. Lembre-se que você deverá desenvolver o cálculo que identifica se um número é primo ou não.

Importante: Aplique a função range().

## *Resposta:*
```
for num in range(100):
    if num == 2 or num == 3 or num == 5 or num == 7:
        print(num)
    elif num % 2 == 0 or num % 3 == 0 or num % 5 == 0 or num == 1 or num % 7 == 0:
        continue
    else:
        print(num)
```

![E4](../../Evidencias/Python_1/Exercicio_4.png)