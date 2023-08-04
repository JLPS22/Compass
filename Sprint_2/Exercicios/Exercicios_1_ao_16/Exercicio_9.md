# E9
Apresente a query para listar o código e nome do produto mais vendido entre as datas de 2014-02-03 até 2018-02-02, e que estas vendas estejam com o status concluída. As colunas presentes no resultado devem ser cdpro e nmpro.

## *Resposta:*
SELECT<br>
	cdpro,<br>
	nmpro<br>

from tbvendas<br>
group by nmpro, cdpro<br>
having (count(dtven between '2014-02-02' and '2018-02-02')) and (lower(status) = 'concluído')<br>
order by count(dtven between '2014-02-02' and '2018-02-02') desc<br>
limit 1

![E9](/Compass/Sprint_2/Evidencias/E9.png)