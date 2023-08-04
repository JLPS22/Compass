# E10
A comissão de um vendedor é definida a partir de um percentual sobre o total de vendas (quantidade * valor unitário) por ele realizado. O percentual de comissão de cada vendedor está armazenado na coluna perccomissao, tabela tbvendedor. 

Com base em tais informações, calcule a comissão de todos os vendedores, considerando todas as vendas armazenadas na base de dados com status concluído.

As colunas presentes no resultado devem ser vendedor, valor_total_vendas e comissao. O valor de comissão deve ser apresentado em ordem decrescente arredondado na segunda casa decimal.

## *Resposta:*
SELECT<br>
	vdd.nmvdd as vendedor,<br>
	sum(ven.qtd * ven.vrunt) as valor_total_vendas,<br>
	round(sum(ven.qtd * ven.vrunt) * vdd.perccomissao/100 ,2) as comissao<br>

from tbvendas as ven<br>
left join tbvendedor as vdd<br>
	on ven.cdvdd = vdd.cdvdd<br>
where lower(ven.status) = 'concluído'<br>
group by vendedor<br>
order by comissao desc