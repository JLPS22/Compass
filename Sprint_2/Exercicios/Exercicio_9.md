# E9
Apresente a query para listar o código e nome do produto mais vendido entre as datas de 2014-02-03 até 2018-02-02, e que estas vendas estejam com o status concluída. As colunas presentes no resultado devem ser cdpro e nmpro.

## Resposta:
SELECT
	cdpro,
	nmpro

from tbvendas
group by nmpro, cdpro
having (count(dtven between '2014-02-02' and '2018-02-02')) and (lower(status) = 'concluído')
order by count(dtven between '2014-02-02' and '2018-02-02') desc
limit 1