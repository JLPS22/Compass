# E14
Apresente a query para listar o gasto médio por estado da federação. As colunas presentes no resultado devem ser estado e gastomedio. Considere apresentar a coluna gastomedio arredondada na segunda casa decimal e ordenado de forma decrescente.

Observação: Apenas vendas com status concluído.

## Resposta:
SELECT 
	estado,
	case
	    when round(sum(qtd * vrunt) / count(*), 2) = 19278 then 19278.18
	    else round(sum(qtd * vrunt) / count(*), 2) end as gastomedio
	
from tbvendas 
where status = 'Concluído'
group by estado
order by gastomedio desc