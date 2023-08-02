# E7
Apresente a query para listar o nome dos autores com nenhuma publicação. Apresentá-los em ordem crescente.

## Resposta:
SELECT
	aut.nome

from autor as aut
left join livro as liv
	on aut.codautor = liv.autor
group by aut.nome
having count(liv.cod) = 0
order by aut.nome