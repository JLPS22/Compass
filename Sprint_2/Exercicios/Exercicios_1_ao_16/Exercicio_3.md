# E3
Apresente a query para listar as 5 editoras com mais livros na biblioteca. O resultado deve conter apenas as colunas quantidade, nome, estado e cidade. Ordenar as linhas pela coluna que representa a quantidade de livros em ordem decrescente.

## *Resposta:*
SELECT<br>
	count(*) as quantidade,<br>
	edt.nome,<br>
	ede.estado,<br>
	ede.cidade<br>

from livro as liv<br>
left join editora as edt<br>
	on liv.editora = edt.codeditora<br>
left join endereco as ede<br>
    on edt.endereco = ede.codendereco<br>
group by edt.nome, ede.estado, ede.cidade<br>
order by quantidade desc<br>
limit 5

![E3](/Compass/Sprint_2/Evidencias/E3.png)