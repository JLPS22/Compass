# E15
Implemente a classe Lampada. A classe Lâmpada recebe um booleano no seu construtor, Truese a lâmpada estiver ligada, False caso esteja desligada. A classe Lampada possuí os seguintes métodos:

liga(): muda o estado da lâmpada para ligada

desliga(): muda o estado da lâmpada para desligada

esta_ligada(): retorna verdadeiro se a lâmpada estiver ligada, falso caso contrário

## *Resposta:*
```
class Lampada:
    def __init__(self, ligada):
        self.ligada = ligada
            
    def liga(self):
        self.ligada = True
        
    def desliga(self):
        self.ligada = False
        
    def esta_ligada(self):
        return self.ligada


lampada = Lampada(False)
print(lampada.esta_ligada())

lampada.liga()
print(lampada.esta_ligada())

lampada.desliga()
print(lampada.esta_ligada())
```

![E15](../../Evidencias/Python_1/Exercicio_15.png)