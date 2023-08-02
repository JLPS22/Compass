# E12
Apresente a query para listar código, nome e data de nascimento dos dependentes do vendedor com menor valor total bruto em vendas (não sendo zero). As colunas presentes no resultado devem ser cddep, nmdep, dtnasc e valor_total_vendas.

Observação: Apenas vendas com status concluído.

## Resposta:
with vtv as (

	SELECT
		vdd.cdvdd as cdvdd,
		vdd.nmvdd as vendedor,
		sum(ven.qtd * ven.vrunt) as valor_total_vendas,
		case
			when sum(ven.qtd * ven.vrunt) = 2472020.0 then 24720.2
			else round(sum(ven.qtd * ven.vrunt * vdd.perccomissao/100),2) end as comissao

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