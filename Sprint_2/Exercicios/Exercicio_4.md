# E4
Apresente a query para listar a quantidade de livros publicada por cada autor. Ordenar as linhas pela coluna nome (autor), em ordem crescente. Além desta, apresentar as colunas codautor, nascimento e quantidade (total de livros de sua autoria).

## Resposta:
SELECT
	nome,
	codautor,
	nascimento,
	count(liv.cod) as quantidade

from autor
left join livro as liv
	on codautor = liv.autor
group by nome, codautor, nascimento
order by nome