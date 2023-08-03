# E1
Apresente a query para listar todos os livros publicados após 2014. Ordenar pela coluna cod, em ordem crescente, as linhas.  Atenção às colunas esperadas no resultado final: cod, titulo, autor, editora, valor, publicacao, edicao, idioma

### Resposta:
SELECT *
FROM livro
WHERE publicacao >= '2015-01-01'
ORDER by cod

# E2
Apresente a query para listar os 10 livros mais caros. Ordenar as linhas pela coluna valor, em ordem decrescente.  Atenção às colunas esperadas no resultado final:  titulo, valor.

### Resposta:
SELECT titulo, valor
FROM livro
order by valor DESC
LIMIT 10

# E3
Apresente a query para listar as 5 editoras com mais livros na biblioteca. O resultado deve conter apenas as colunas quantidade, nome, estado e cidade. Ordenar as linhas pela coluna que representa a quantidade de livros em ordem decrescente.

### Resposta:
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

# E4
Apresente a query para listar a quantidade de livros publicada por cada autor. Ordenar as linhas pela coluna nome (autor), em ordem crescente. Além desta, apresentar as colunas codautor, nascimento e quantidade (total de livros de sua autoria).

### Resposta:
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

# E5
Apresente a query para listar o nome dos autores que publicaram livros através de editoras NÃO situadas na região sul do Brasil. Ordene o resultado pela coluna nome, em ordem crescente. Não podem haver nomes repetidos em seu retorno.

### Resposta:
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

# E6
Apresente a query para listar o autor com maior número de livros publicados. O resultado deve conter apenas as colunas codautor, nome, quantidade_publicacoes.

### Resposta:
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

# E7
Apresente a query para listar o nome dos autores com nenhuma publicação. Apresentá-los em ordem crescente.

### Resposta:
SELECT
	aut.nome

from autor as aut
left join livro as liv
	on aut.codautor = liv.autor
group by aut.nome
having count(liv.cod) = 0
order by aut.nome

# E8
Apresente a query para listar o código e o nome do vendedor com maior número de vendas (contagem), e que estas vendas estejam com o status concluída.  As colunas presentes no resultado devem ser, portanto, cdvdd e nmvdd.

### Resposta:
SELECT
	vdr.cdvdd,
	vdr.nmvdd

from tbvendas as vendas
left join tbvendedor as vdr
	on vendas.cdvdd = vdr.cdvdd
group by vdr.cdvdd, vdr.nmvdd
order by count(vendas.qtd) desc
limit 1

# E9
Apresente a query para listar o código e nome do produto mais vendido entre as datas de 2014-02-03 até 2018-02-02, e que estas vendas estejam com o status concluída. As colunas presentes no resultado devem ser cdpro e nmpro.

### Resposta:
SELECT
	cdpro,
	nmpro

from tbvendas
group by nmpro, cdpro
having (count(dtven between '2014-02-02' and '2018-02-02')) and (lower(status) = 'concluído')
order by count(dtven between '2014-02-02' and '2018-02-02') desc
limit 1

# E10
A comissão de um vendedor é definida a partir de um percentual sobre o total de vendas (quantidade * valor unitário) por ele realizado. O percentual de comissão de cada vendedor está armazenado na coluna perccomissao, tabela tbvendedor. 

Com base em tais informações, calcule a comissão de todos os vendedores, considerando todas as vendas armazenadas na base de dados com status concluído.

As colunas presentes no resultado devem ser vendedor, valor_total_vendas e comissao. O valor de comissão deve ser apresentado em ordem decrescente arredondado na segunda casa decimal.

### Resposta:
SELECT
	vdd.nmvdd as vendedor,
	sum(ven.qtd * ven.vrunt) as valor_total_vendas,
	round(sum(ven.qtd * ven.vrunt) * vdd.perccomissao/100 ,2) as comissao

from tbvendas as ven
left join tbvendedor as vdd
	on ven.cdvdd = vdd.cdvdd
where lower(ven.status) = 'concluído'
group by vendedor
order by comissao desc

# E11
Apresente a query para listar o código e nome cliente com maior gasto na loja. As colunas presentes no resultado devem ser cdcli, nmcli e gasto, esta última representando o somatório das vendas (concluídas) atribuídas ao cliente.

### Resposta:
SELECT
	cdcli,
	nmcli,
	sum(tbvendas.qtd * tbvendas.vrunt) as gasto

from tbvendas
group by cdcli, nmcli
order by gasto desc
limit 1

# E12
Apresente a query para listar código, nome e data de nascimento dos dependentes do vendedor com menor valor total bruto em vendas (não sendo zero). As colunas presentes no resultado devem ser cddep, nmdep, dtnasc e valor_total_vendas.

Observação: Apenas vendas com status concluído.

### Resposta:
with vtv as (
	SELECT
		vdd.cdvdd as cdvdd,
		vdd.nmvdd as vendedor,
		sum(ven.qtd * ven.vrunt) as valor_total_vendas,
		round(sum(ven.qtd * ven.vrunt) * vdd.perccomissao/100 ,2) as comissao
		
	from tbvendas as ven
	left join tbvendedor as vdd
		on ven.cdvdd = vdd.cdvdd
	where lower(ven.status) = 'concluído'
	group by vendedor
)

SELECT
	dep.cddep,
	dep.nmdep,
	dep.dtnasc,
	min(vtv.valor_total_vendas) as valor_total_vendas

from vtv
left join tbdependente as dep
	on vtv.cdvdd = dep.cdvdd
group by dep.cddep, dep.nmdep, dep.dtnasc
order by valor_total_vendas
limit 1

# E13
Apresente a query para listar os 10 produtos menos vendidos pelos canais de E-Commerce ou Matriz (Considerar apenas vendas concluídas).  As colunas presentes no resultado devem ser cdpro, nmcanalvendas, nmpro e quantidade_vendas.

### Resposta:
SELECT
	cdpro,
	nmcanalvendas,
	nmpro,
	sum(qtd) as quantidade_vendas

from tbvendas
where (nmcanalvendas = 'Matriz' or nmcanalvendas = 'Ecommerce') and (status = 'Concluído')
group by cdpro, nmcanalvendas, nmpro
order by quantidade_vendas

# E14
Apresente a query para listar o gasto médio por estado da federação. As colunas presentes no resultado devem ser estado e gastomedio. Considere apresentar a coluna gastomedio arredondada na segunda casa decimal e ordenado de forma decrescente.

Observação: Apenas vendas com status concluído.

### Resposta:
SELECT 
	estado,
	round(avg(qtd * vrunt), 2) as gastomedio
	
from tbvendas 
where status = 'Concluído'
group by estado
order by gastomedio desc

# E15
Apresente a query para listar os códigos das vendas identificadas como deletadas. Apresente o resultado em ordem crescente.

### Resposta:
SELECT 
    cdven

from tbvendas
where deletado >= 1
order by cdven

# E16
Apresente a query para listar a quantidade média vendida de cada produto agrupado por estado da federação. As colunas presentes no resultado devem ser estado e nmprod e quantidade_media. Considere arredondar o valor da coluna quantidade_media na quarta casa decimal. Ordene os resultados pelo estado (1º) e nome do produto (2º).

Obs: Somente vendas concluídas.

## Resposta:
SELECT
	estado,
	nmpro,
	round(avg(qtd), 4) as quantidade_media

from tbvendas
where status = 'Concluído'
group by estado, nmpro
order by estado, nmpro
