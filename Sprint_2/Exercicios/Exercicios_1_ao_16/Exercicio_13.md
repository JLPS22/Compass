# E13
Apresente a query para listar os 10 produtos menos vendidos pelos canais de E-Commerce ou Matriz (Considerar apenas vendas concluídas).  As colunas presentes no resultado devem ser cdpro, nmcanalvendas, nmpro e quantidade_vendas.

## *Resposta:*
SELECT<br>
	cdpro,<br>
	nmcanalvendas,<br>
	nmpro,<br>
	sum(qtd) as quantidade_vendas

from tbvendas<br>
where (nmcanalvendas = 'Matriz' or nmcanalvendas = 'Ecommerce') and (status = 'Concluído')<br>
group by cdpro, nmcanalvendas, nmpro<br>
order by quantidade_vendas

![E13](/Compass/Sprint_2/Evidencias/E13.png)