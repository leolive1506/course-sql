# Banco de dados
* Objetivo do banco de dados: Registrar instâncias seperadas com caracteristicas semelhantes
* *Banco*: Coleções de dados
    * *Tabelas*: Locais com os dados (conjunto de registros) que contém campos
    * Dados dentro da tabela chamam *REGISTROS*



# Tipos Primitivos
* *Numérico* (diferença está qtd de bytes vai utilizar para armazenar o dado, influência no tamanho do dado que vai guardar)
    * Inteiro
        * TinyInt (3 bytes)
        * SmallInt
        * Int (11 bytes)
        * MidiumInt
        * BigInt

    * Real 
        * Decimal
            * decimal(total_de_casas, numeros_apos_virgula)
                * decimal(5,2)
                        * ex: 102,32
        * Float
        * Double
        * Real 

    * Lógico (sim e não, false e true, 0 e 1)
        * Bit
        * Boolean

* *Data / Tempo*
    * Date (data)
    * DateTime (data, horas e informaçoes a mais)
    * TimeStamp (data, horas e informaçoes a mais)
    * Time (hora)
    * Year (ano)

* *Literal*
    * Caractere
        * Char (fixo)
            * Ocupa os espaços fixos
        * VarChar (variante)
            * Define um tamanho mas pode variar pra menos

    * Texto 
        * TinyText 
        * Text
        * MediuText
        * LongText

    * `Diferença entre caractere e texto -> texto: longos, caractere: +curto`

    * Binário (guardar qualquer coisa em binário -> Ex: Img)
        * TinyBlob
        * Blob
        * MediuBlob
        * LongBlob

    * Coleção (config valores permitidos)
        * Enum
            * Enum('M', 'F')
        * Set

* *Espaciais* (cadastro de algo volumetrico)
    * Geometry
    * Point
    * Polygon
    * MultiPolygon

# Geral
* Acessar no terminal
```sh
mysql -uroot -proot
```

```sql
show databases;
use databaseDesejada
show tables

```

* Mostrar estrutura da table
```sql
describe pessoas;
desc pessoas;
```

* Quando quiser salvar idade colocar data de nascimento, pq a idade muda mas a data não

* Chave primaria -> Valor único na tabela

* UNIQUE
    * Não permite repetir o valor (não é primary key)

* int UNSIGNED
    * Não permite sinal

* Registros ou tupla é a mesma coisa que linha

# Comandos

* Comando para criar database
```sql
create database nameDatabase character set utf8 collate utf8_unicode_ci;
```

* Comando criar table
```sql
CREATE TABLE IF NOT EXISTS nameTable (
    id int NOT NULL AUTO_INCREMENT,
    nome varchar(30) NOT NULL,
    nascimento date,
    sexo enum('M','F'),
    peso decimal(5,2),
    altura decimal(3,2),
    nacionalidade varchar(20) DEFAULT 'Brasil',
    PRIMARY KEY (id)
);
```

* Apagar uma Table
```sql
drop database cadastro;
```

* Inserir Dados em uma tabela
```sql
insert into tableDesejada (campo1, campo2, campo2...)
values ('value1', 'value2', 'value3'...)
```
    * Se a ordem dos campos a serem inseridos forem o mesmo, pode omitor os campo
        ex: 
```sql
-- table so com nome e cpf
insert into tableDesejada (nome, cpf)
values 
    ('Leo', '1324-51923-9'),
    ('Patrick', '3324-51923-9'),
    ('Creuza', '5324-51923-9'),

-- mesmo que
insert into tableDesejada values ('Leo', '1324-51923-9')
```

* *Alterar tabela*

* Adicionar coluna
```sql
ALTER TABLE nameTable
ADD COLUMN nameColumn varchar(10); 
```

* Remover coluna

```sql
ALTER TABLE nameTable
DROP COLUMN nameColumn;
```

* Escolher posiçao para add a coluna
```sql
ALTER TABLE pessoas ADD COLUMN nome_da_coluna_ser_add varchar(10) AFTER nome_da_coluna_de_referencia_para_inserir;
```

* Adicionar como primeiro campo
```sql
ALTER TABLE pessoas ADD COLUMN nome_da_coluna_ser_add int FIRST;
```

* Alterar estrutura de um campo
```sql
ALTER TABLE nome_table MODIFY COLUMN nome_da_coluna_ser_modificada varchar(30);
```

* Alterar NOME da coluna
```sql
ALTER TABLE nome_da_table CHANGE COLUMN nome_antigo_da_coluna nome_novo_da_coluna varchar(30) NOT NULL DEFAULT '';
```

* Renomear a table inteira
```sql
ALTER TABLE nome_antigo_table RENAME TO nome_novo_da_coluna;
```

* Adicionar chave primaria a uma column
```sql
ALTER TABLE nome_tabela ADD COLUMN id int FIST;

ALTER TABLE nome_table ADD PRIMARY KEY (id);
```

* Alterar linha (registro ou tupla)
```sql
UPDATE nome_da_tabela 
SET campo_da_tabela_que_sofrera_mudanca1 = 'novoValor1', 
    campo_da_tabela_que_sofrera_mudanca2 = 'novoValor2' where condicao;
```

    * Limitar quantas linhas vão ser afetadas
```sql
UPDATE cursos set nome = 'php' where id = '1' LIMIT 1
```

* Remover linhas
```sql
DELETE FROM nome_da_table WHERE condicao;
-- limitar quantidade
DELETE FROM nome_da_table WHERE condicao LIMIT 3;
```


* Apagar todos os registros / dados / linha de uma tabela
```sql
TRUNCATE TABLE nome_da_table_que_vai_remover_as_linhas;

-- mesma coisa
TRUNCATE nome_da_table_que_vai_remover_as_linhas;
```

# SELECT
* Escolher a ordem da seleção
```sql
SELECT * FROM nome_da_table ORDER BY nome_campo_que_vai_seguir_a_ordem;

-- MESMA COISA ACIMA
SELECT * FROM nome_da_table ORDER BY nome_campo_que_vai_seguir_a_ordem ASC;


-- COMEÇA COM MAIOR(NUM) OU ULTIMA LETRA(TEXT)
SELECT * FROM nome_da_table ORDER BY nome_campo_que_vai_seguir_a_ordem DESC;

-- mais de um campo
SELECT ano, nome, cpf FROM nome_da_table ORDER BY id, nome
```

* Selecionar com condição
```sql
SELECT * FROM nome_da_table WHERE condicao ORDER BY campo_que_vai_dar_base_p_ordem;

SELECT * FROM nome_da_table WHERE condicao1 AND condicao2 ORDER BY campo_que_vai_dar_base_p_ordem;

SELECT * FROM nome_da_table WHERE condicao1 OR condicao2 ORDER BY campo_que_vai_dar_base_p_ordem;

```

* Selecionar entre, valores especificos
```sql
-- entre
SELECT nome, ano FROM nome_da_table WHERE ano BETWEEN 2014 AND 2016;

-- valores especificos
SELECT ano, nome FROM cursos where ano IN ('2022', '2021');
```

* Like
```sql
SELECT * FROM nome_da_table WHERE nome like 'a%';
SELECT * FROM nome_da_table WHERE nome like '%a';

-- ACHAR EM QUALQUER LUGAR
SELECT * FROM nome_da_table WHERE nome like '%a%';

-- NÃO PEGA OS QEU COMEÇA COM 'A'
SELECT * FROM nome_da_table WHERE nome NOT like 'a%';

-- PEGA OS QUE COMEÇAM COM 'PH' E TERMINAL COM 'P'
    -- EX: PHP, PHOTOSHOP

SELECT * FROM cursos WHERE nome LIKE 'PH%P';

-- PARA OBRIGAR QUE TENHA UM CARACTER ANTES OU DPS USAR "_"
    --  No final tem algo dps do p
    -- ex: php4
SELECT * FROM nome_da_table WHERE nome like 'php%p_';
    -- No começo tem algo antes do p e termina com p
select * from cursos where nome like '%_p';

```

* Distinguindo
    * Não permite selecionar repetição, pega so um
    * Ex: Tabela com muitos usuários de diferentes paises onde muitos paises se repetem varias vezes. Usando DISTINCT ele não deixa repetir o pais na busca e lista os paises de onde os users moram
    ```sql
    SELECT DISTINCT nacionalidade from tabela_que_quer_selecionar ORDER BY nacionalidade;
    ```

* Funções de Agregação
    * COUNT - Selecionar ou totalizar alguma coisa
    ```sql
    -- Lista quantos nomes tem na tabela (se a table for muito grande pode levar tempo pra chegar no ultimo)
    select count(nome) from cursos;

    -- Conta as cargas maiores que 40
    select count(*) from cursos where carga > 40;
    ```

    * MAX(campo) - pega o valor max de um campo
    ```sql
    select max(carga) from cursos;
    select max(totaulas) from cursos where ano = '2021';
    ```

    * MIN(campo) - pega o valor min de um campo
    ```sql
    select min(totaulas) from cursos where ano = '2021';
    ```

    * SUM(campo) - somar
    ```sql
    select sum(totaulas) from cursos where ano = '2016'
    ```

    * AVG(campo) - Tirar a média
        * Soma tudo e divide pelo número de items
    ```sql
    select AVG(totaulas) from cursos where;
    ```

# Exercício
```sql
-- 1) Uma lista com o nome de todos os gafanhotos Mulheres.

select nome from gafanhotos where sexo="f";

-- 2) Uma lista com os dados de todos aqueles que nasceram entre 1/Jan/2000 e 31/Dez/2015.

select * from gafanhotos where nascimento between '2000-01-01' and '2015-12-31';

-- 3) Uma lista com o nome de todos os homens que trabalham como programadores.
select nome from gafanhotos where prof = 'programador';

-- 4) Uma lista com os dados de todas as mulheres que nasceram no Brasil e que têm seu nome iniciando com a letra J.
select * from gafanhotos where nacionalidade = 'Brasil' and nome like 'j%';

-- 5) Uma lista com o nome e nacionalidade de todos os homens que têm Silva no nome, não nasceram no Brasil e pesam menos de 100 Kg.
select nome, nacionalidade from gafanhotos where sexo = 'M' and nacionalidade != 'Brasil' and peso < '100';

-- 6) Qual é a maior altura entre gafanhotos Homens que moram no Brasil?
select max(altura) from gafanhotos where nacionalidade = 'Brasil';

-- 7) Qual é a média de peso dos gafanhotos cadastrados?
select avg(peso) from gafanhotos;

-- 8) Qual é o menor peso entre os gafanhotos Mulheres que nasceram fora do Brasil e entre 01/Jan/1990 e 31/Dez/2000?
select min(peso) from gafanhotos where sexo = 'F' and nacionalidade <> 'brasil' and nascimento BETWEEN '1990-01-01' and '2000-12-31';
             

-- 9) Quantas gafanhotos Mulheres tem mais de 1.90cm de altura?
select * from gafanhotos where sexo = 'F' and altura > '1.90';
```