# E12
Apresente a query para listar código, nome e data de nascimento dos dependentes do vendedor com menor valor total bruto em vendas (não sendo zero). As colunas presentes no resultado devem ser cddep, nmdep, dtnasc e valor_total_vendas.

Observação: Apenas vendas com status concluído.

## *Resposta:*
with vtv as (<br>
	SELECT<br>
		vdd.cdvdd as cdvdd,<br>
		vdd.nmvdd as vendedor,<br>
		sum(ven.qtd * ven.vrunt) as valor_total_vendas,<br>
		round(sum(ven.qtd * ven.vrunt) * vdd.perccomissao/100 ,2) as comissao
		
	from tbvendas as ven
	left join tbvendedor as vdd
		on ven.cdvdd = vdd.cdvdd
	where lower(ven.status) = 'concluído'
	group by vendedor
)

SELECT<br>
	dep.cddep,<br>
	dep.nmdep,<br>
	dep.dtnasc,<br>
	min(vtv.valor_total_vendas) as valor_total_vendas

from vtv<br>
left join tbdependente as dep<br>
	on vtv.cdvdd = dep.cdvdd<br>
group by dep.cddep, dep.nmdep, dep.dtnasc<br>
order by valor_total_vendas<br>
limit 1

![E12](/Compass/Sprint_2/Evidencias/E12.png)