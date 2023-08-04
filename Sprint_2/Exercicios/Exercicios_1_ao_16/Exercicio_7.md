# E7
Apresente a query para listar o nome dos autores com nenhuma publicação. Apresentá-los em ordem crescente.

## *Resposta:*
SELECT<br>
	aut.nome<br>

from autor as aut<br>
left join livro as liv<br>
	on aut.codautor = liv.autor<br>
group by aut.nome<br>
having count(liv.cod) = 0<br>
order by aut.nome