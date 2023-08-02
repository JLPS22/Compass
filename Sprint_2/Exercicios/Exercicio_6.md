# E6
Apresente a query para listar o autor com maior número de livros publicados. O resultado deve conter apenas as colunas codautor, nome, quantidade_publicacoes.

## Resposta:
SELECT
	aut.codautor,
	aut.nome,
	count(*) as quantidade_publicacoes

from livro as liv
left join autor as aut
	on liv.autor = aut.codautor
group by aut.codautor, aut.nome
order by quantidade_publicacoes desc
limit 1