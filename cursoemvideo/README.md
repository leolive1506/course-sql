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