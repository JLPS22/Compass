# E3
Apresente a query para listar as 5 editoras com mais livros na biblioteca. O resultado deve conter apenas as colunas quantidade, nome, estado e cidade. Ordenar as linhas pela coluna que representa a quantidade de livros em ordem decrescente.

## Resposta:
SELECT
	count(*) as quantidade,
	edt.nome,
	ede.estado,
	ede.cidade

from livro as liv
left join editora as edt
	on liv.editora = edt.codeditora
left join endereco as ede
	on edt.endereco = ede.codendereco
group by edt.nome, ede.estado, ede.cidade
order by quantidade desc
limit 5