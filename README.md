
# Resolução exercício SQL

1ª Abra o arquivo ´banco_produtos.txt´ acima e copie e cole no SGBD
PostgreSQL, utilizando a ferramenta PgAdmin4 no seu computador.


## 1ª Questão
A - Pesquise os itens que foram vendidos sem desconto. As colunas presentes no resultado da
consulta são: ID_NF, ID_ITEM, COD_PROD E VALOR_UNIT.

```sql
select id_nf, id_item, cod_prod, valor_unit 
from produtos
where desconto is null;
```
## Resultado esperado

![q1](https://user-images.githubusercontent.com/6910054/204104098-b7cdae85-ee7c-46bf-976e-43c848686e35.PNG)

## 2ª Questão
B -Pesquise os itens que foram vendidos com desconto. As colunas presentes no resultado da
consulta são: ID_NF, ID_ITEM, COD_PROD, VALOR_UNIT E O VALOR VENDIDO.

```sql
select id_nf, id_item, cod_prod, valor_unit, valor_unit - (valor_unit * desconto/100) as valor_vendido
from produtos
where desconto is not null;
```
## Resultado esperado

![q2](https://user-images.githubusercontent.com/6910054/204104683-b2db8d82-81f6-4376-a028-1f9ce0513edb.PNG)

## 3ª Questão
C - Altere o valor do desconto (para zero) de todos os registros onde este campo é nulo.

```sql
update produtos set desconto=0 where desconto is null;
```
