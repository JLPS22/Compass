# E15
Apresente a query para listar os códigos das vendas identificadas como deletadas. Apresente o resultado em ordem crescente.

## Resposta:
SELECT 
    cdven

from tbvendas
where deletado >= 1
order by cdven