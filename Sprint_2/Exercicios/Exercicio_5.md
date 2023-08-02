# E5
Apresente a query para listar o nome dos autores que publicaram livros através de editoras NÃO situadas na região sul do Brasil. Ordene o resultado pela coluna nome, em ordem crescente. Não podem haver nomes repetidos em seu retorno.

## Resposta:
SELECT DISTINCT aut.nome

FROM livro as liv
left join autor as aut
	on liv.autor = aut.codautor
left join editora as edt
	on liv.editora = edt.codeditora
left join endereco as ede
	on edt.endereco = ede.codendereco
where ede.estado not in ('PARANÁ', 'RIO GRANDE DO SUL')
order by aut.nome