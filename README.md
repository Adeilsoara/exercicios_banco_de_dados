
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

## 4ª Questão
D - Pesquise os itens que foram vendidos. As colunas presentes no resultado da consulta
são: ID_NF, ID_ITEM, COD_PROD, VALOR_UNIT, VALOR_TOTAL, DESCONTO, VALOR_VENDIDO. 
OBS: O VALOR_TOTAL é obtido pela fórmula: QUANTIDADE * VALOR_UNIT.
O VALOR_VENDIDO é igual a VALOR_UNIT - (VALOR_UNIT*(DESCONTO/100)).

```sql
select id_nf, id_item, cod_prod, valor_unit,
       valor_unit - (valor_unit * desconto/100) as valor_com_desconto,
       quantidade * valor_unit as valor_total
from produtos;
```
## Resultado esperado

![q4](https://user-images.githubusercontent.com/6910054/204105209-36056f9e-782a-4ade-9802-c19431d0afcd.PNG)

## 5ª Questão
E - Pesquise o valor total das NF e ordene o resultado do maior valor para o menor. As
colunas presentes no resultado da consulta são: ID_NF, VALOR_TOTAL. 
OBS: OVALOR_TOTAL é obtido pela fórmula: Σ QUANTIDADE * VALOR_UNIT. 
Agrupe o resultado da consulta por ID_NF.

```sql
select id_nf, sum(quantidade * valor_unit ) as valor_total 
from produtos 
group by id_nf 
order by valor_total desc;
```
## Resultado esperado

![q5](https://user-images.githubusercontent.com/6910054/204105402-13e9d737-7d57-42d0-955a-58447fd5127b.PNG)

## 6ª Questão
F - Pesquise o valor vendido das NF e ordene o resultado do maior valor para o menor. As
colunas presentes no resultado da consulta são: ID_NF, VALOR_VENDIDO.
OBS:
O VALOR_TOTAL é obtido pela fórmula: Σ QUANTIDADE * VALOR_UNIT.
O VALOR_VENDIDO é igual a Σ VALOR_UNIT - (VALOR_UNIT*(DESCONTO/100)).
Agrupe o resultado da consulta por ID_NF.

```sql
select id_nf, sum(valor_unit - (valor_unit *(desconto/100))) as valor_vendido 
from produtos 
group by id_nf 
order by valor_vendido desc;
```
## Resultado esperado

![q6](https://user-images.githubusercontent.com/6910054/204105601-c7dc556a-67f1-44aa-b020-b7ff315121a8.PNG)

## 7ª Questão
G - Consulte o produto que mais vendeu no geral. As colunas presentes no resultado da consulta
são: COD_PROD, QUANTIDADE. Agrupe o resultado da consulta por COD_PROD.

```sql
select cod_prod, sum(quantidade) as qtd_total 
from produtos 
group by cod_prod 
order by qtd_total desc;
```
## Resultado esperado

![q7](https://user-images.githubusercontent.com/6910054/204105755-7160e5ca-5585-486d-8727-08a475f0d87e.PNG)

## 8ª Questão
H - Consulte as NF que foram vendidas mais de 10 unidades de pelo menos um produto.
As colunas presentes no resultado da consulta são: ID_NF, COD_PROD, QUANTIDADE.

```sql
select id_nf, cod_prod, sum(quantidade) as quantidade
from produtos
where quantidade > 10
group by id_nf, cod_prod
```
## Resultado esperado

![q8](https://user-images.githubusercontent.com/6910054/204105935-171ea319-d0eb-4a4b-b143-44d399367ce6.PNG)


## 9ª Questão
I - Pesquise o valor total das NF, onde esse valor seja maior que 500, e ordene o resultado do
maior valor para o menor. As colunas presentes no resultado da consulta são: ID_NF,
VALOR_TOT. OBS: O VALOR_TOTAL é obtido pela fórmula: Σ QUANTIDADE * VALOR_UNIT.
Agrupe o resultado da consulta por ID_NF.

```sql
select id_nf, sum(quantidade * valor_unit) as valor_total
from produtos
group by id_nf
having sum(quantidade * valor_unit) > 500;
```
## Resultado esperado

![q9](https://user-images.githubusercontent.com/6910054/204106094-6e474e4c-36f2-4008-93d9-b5fc51b75c13.PNG)

## 10ª Questão
J - Qual o valor médio dos descontos dados por produto. As colunas presentes no resultado da
consulta são: COD_PROD, MEDIA. Agrupe o resultado da consulta por COD_PROD.

```sql
select cod_prod, avg(quantidade * (valor_unit - (valor_unit *(desconto/100)))) as media 
from produtos 
group by cod_prod;
```
## Resultado esperado

![q10](https://user-images.githubusercontent.com/6910054/204106384-469670df-ee12-4627-9a1a-1d883f74cc7b.PNG)

## 11ª Questão
K - Qual o menor, maior e o valor médio dos descontos dados por produto. As colunas
presentes no resultado da consulta são: COD_PROD, MENOR, MAIOR, MEDIA. Agrupe
o resultado da consulta por COD_PROD.

```sql
select cod_prod,
avg(desconto) as media_desconto, 
min(desconto) as menor_desconto,
max(desconto) as maior_desconto
from produtos
group by cod_prod;
```
## Resultado esperado

![q11](https://user-images.githubusercontent.com/6910054/204106514-4f2b5eca-b3f9-4c61-acb5-8de8e7e44cc8.PNG)

## 12ª Questão
L - Quais as NF que possuem mais de 3 itens vendidos. As colunas presentes no resultado
da consulta são: ID_NF, QTD_ITENS. OBS:: NÃO ESTÁ RELACIONADO A QUANTIDADE
VENDIDA DO ITEM E SIM A QUANTIDADE DE ITENS POR NOTA FISCAL. Agrupe o
resultado da consulta por ID_NF.

```sql
select id_nf, sum(quantidade) as qtd_itens 
from produtos 
where quantidade > 3 
group by id_nf 
order by qtd_itens desc;
```
## Resultado esperado

![q12](https://user-images.githubusercontent.com/6910054/204106642-12e33b17-7ae7-4d6f-9764-5c4f5e32a3b4.PNG)

