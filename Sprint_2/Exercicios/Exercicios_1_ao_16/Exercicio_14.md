# E14
Apresente a query para listar o gasto médio por estado da federação. As colunas presentes no resultado devem ser estado e gastomedio. Considere apresentar a coluna gastomedio arredondada na segunda casa decimal e ordenado de forma decrescente.

Observação: Apenas vendas com status concluído.

## *Resposta:*
SELECT <br>
	estado,<br>
	round(avg(qtd * vrunt), 2) as gastomedio
	
from tbvendas<br>
where status = 'Concluído'<br>
group by estado<br>
order by gastomedio desc

![E14](/Compass/Sprint_2/Evidencias/E14.png)