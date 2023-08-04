# E15
Apresente a query para listar os códigos das vendas identificadas como deletadas. Apresente o resultado em ordem crescente.

## *Resposta:*
SELECT<br>
    cdven

from tbvendas<br>
where deletado >= 1<br>
order by cdven

![E15](/Compass/Sprint_2/Evidencias/E15.png)