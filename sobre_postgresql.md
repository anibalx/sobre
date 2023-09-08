# ACESSO AO POSTGRES
> Aqui, usa-se o comando sudo, mas não é sempre necessário
```sh
  sudo -U postgres psql
```

# CRIAÇÃO DE BANCO DE DADOS
```sh
  create database mytest;
```

# LISTA OS BANCOS DE DADOS
```sh
  \l
```

# CONECTE A UM BANCO DE DADOS
```sh
  \c mytest
```

# CRIAÇÂO DE TIPO ESPCÌFICO
```sh
  create type cat_enum AS ENUM ('coffe', 'tea');
```

# LISTA OS TIPOS DE DADOS
```sh
  \dT+
```

# CRIAÇÂO DE TABELAS
```sh
create table if not exists cafe (
id SERIAL PRIMARY KEY,        -- AUTO_INCREMENT integer, as primary key
category cat_enum NOT NULL,   -- Use the enum type defined earlier
name VARCHAR(50) NOT NULL,    -- Variable-length string of up to 50 characters
price NUMERIC(5,2) NOT NULL,  -- 5 digits total, with 2 decimal places
last_update DATE              -- 'YYYY-MM-DD'
    );
```

# USO O COMANDO SELECT
```sh
  select * from cafe;
```

# USO O COMANDO INSERT
```sh
    insert into cafe (category, name, price) VALUES (
    ('coffee', 'Expresso', 3.19),
    ('coffee', 'Cappuccino', 3.29),
    ('coffee', 'Caffe Latte', 3.39),
    ('coffee', 'Caffe Mocha', 3.49),
    ('coffee', 'Brewed Coffe', 3.59),
    ('tea', 'Expresso', 2.99),
    ('tea', 'Expresso', 2.89),
        );
```

# USO O COMANDO UPDATE
```sh
  update cafe SET price = price * 1.1 WHERE category = 'tea';
```

# USO O COMANDO DELETE
```sh
  delete from cafe where id = 0;
```

# CRIAÇÂO DE VIEW
```sh
    CREATE MATERIALIZED VIEW minha_view
    AS
    SELECT CL.nome_cliente, PR.nome_produto, PE.qtde
    FROM pedidos PE
    INNER JOIN clientes CL
    ON PE.cod_cliente = CL.cod_cliente
    INNER JOIN produtos PR
    ON PE.cod_produto = PR.cod_produto
    ORDER BY CL.nome_cliente
    WITH NO DATA;
```

# POPULAÇÂO DA VIEW
```sh
    REFRESH MATERIALIZED VIEW minha_view
```

# ALTERAÇÃO DA VIEW
```sh
    ALTER MATERIALIZED VIEW minha_view
    RENAME COLUMN nome_produto TO Produto;
```

# EXCLUIR A VIEW
```sh
    DROP MATERIALIZED VIEW minha_view
```

# SUBCONSULTA
## SELECT
```sh
    -- Nome e preço do livro mais caro
    SELECT nome_livro, preco_livro
    FROM tbl_livros
    WHERE preco_livro = (
        SELECT MAX(preco_livro)
        FROM tbl_livros
    );
```

```sh
    -- Nome e preço de livro de acordo com nome de editora conhecido
    SELECT nome_livro, preco_livro, editora
    FROM tbl_livros
    WHERE editora = (
        SELECT id_editora
        FROM tbi_editoras
        WHERE nome_editora = 'Wiley'
    );
```

```sh
    -- Nome e preço de livro de acordo com nome das editoras conhecidas
    SELECT nome_livro, preco_livro, editora
    FROM tbl_livros
    WHERE editora IN (
        SELECT id_editora
        FROM tbi_editoras
        WHERE nome_editora = 'Wiley' OR nome_editora = 'Prentice Hall'
    );
```

## UPDATE
```sh
    -- Atualiza os preços dos livros da editora Microsoft em +15%
    UPDATE tbl_livros
    SET preco_livro = preco_livro * 1.15
    WHERE editora = (
        SELECT id_editora
        FROM tbl_editoras
        WHERE nome_editora LIKE '%Microsoft%'
    );
```
