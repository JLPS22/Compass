# E2
Apresente a query para listar os 10 livros mais caros. Ordenar as linhas pela coluna valor, em ordem decrescente.  Atenção às colunas esperadas no resultado final:  titulo, valor.

## Resposta:
SELECT titulo, valor
FROM livro
order by valor DESC
LIMIT 10