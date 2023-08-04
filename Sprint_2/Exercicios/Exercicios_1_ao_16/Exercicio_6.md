# E6
Apresente a query para listar o autor com maior número de livros publicados. O resultado deve conter apenas as colunas codautor, nome, quantidade_publicacoes.

## *Resposta:*
SELECT<br>
	aut.codautor,<br>
	aut.nome,<br>
	count(*) as quantidade_publicacoes<br>

from livro as liv<br>
left join autor as aut<br>
	on liv.autor = aut.codautor<br>
group by aut.codautor, aut.nome<br>
order by quantidade_publicacoes desc<br>
limit 1