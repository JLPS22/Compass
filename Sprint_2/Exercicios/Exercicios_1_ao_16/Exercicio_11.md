# E11
Apresente a query para listar o código e nome cliente com maior gasto na loja. As colunas presentes no resultado devem ser cdcli, nmcli e gasto, esta última representando o somatório das vendas (concluídas) atribuídas ao cliente.

## *Resposta:*
SELECT<br>
	cdcli,<br>
	nmcli,<br>
	sum(tbvendas.qtd * tbvendas.vrunt) as gasto<br>

from tbvendas<br>
group by cdcli, nmcli<br>
order by gasto desc<br>
limit 1

![E11](/Compass/Sprint_2/Evidencias/E11.png)