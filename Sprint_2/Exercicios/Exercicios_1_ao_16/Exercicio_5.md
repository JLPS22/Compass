# E5
Apresente a query para listar o nome dos autores que publicaram livros através de editoras NÃO situadas na região sul do Brasil. Ordene o resultado pela coluna nome, em ordem crescente. Não podem haver nomes repetidos em seu retorno.

## *Resposta:*
SELECT DISTINCT aut.nome

FROM livro as liv<br>
left join autor as aut<br>
	on liv.autor = aut.codautor<br>
left join editora as edt<br>
	on liv.editora = edt.codeditora<br>
left join endereco as ede<br>
	on edt.endereco = ede.codendereco<br>
where ede.estado not in ('PARANÁ', 'RIO GRANDE DO SUL')<br>
order by aut.nome