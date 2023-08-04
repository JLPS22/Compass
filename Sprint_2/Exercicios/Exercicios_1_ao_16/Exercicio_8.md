# E8
Apresente a query para listar o código e o nome do vendedor com maior número de vendas (contagem), e que estas vendas estejam com o status concluída.  As colunas presentes no resultado devem ser, portanto, cdvdd e nmvdd.

## *Resposta:*
SELECT<br>
	vdr.cdvdd,<br>
	vdr.nmvdd

from tbvendas as vendas<br>
left join tbvendedor as vdr<br>
	on vendas.cdvdd = vdr.cdvdd<br>
group by vdr.cdvdd, vdr.nmvdd<br>
order by count(vendas.qtd) desc<br>
limit 1