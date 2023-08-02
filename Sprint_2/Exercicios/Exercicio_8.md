# E8
Apresente a query para listar o código e o nome do vendedor com maior número de vendas (contagem), e que estas vendas estejam com o status concluída.  As colunas presentes no resultado devem ser, portanto, cdvdd e nmvdd.

## Resposta:
SELECT
	vdr.cdvdd,
	vdr.nmvdd

from tbvendas as vendas
left join tbvendedor as vdr
	on vendas.cdvdd = vdr.cdvdd
group by vdr.cdvdd, vdr.nmvdd
order by count(vendas.qtd) desc
limit 1