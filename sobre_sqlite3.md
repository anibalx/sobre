# CRIA BANCO DE DADOS DENTRO DO SQLITE3
```
  sqlite> .open my_database.db
```

# EXIBE OS BANCOS DE DADOS ABERTOS DENTRO DO SQLITE3
```
  sqlite> .databases
```

# CRIAÇÃO DE TABELA DENTRO DO SQLITE3
```
	 sqlite> create table memos(text, priority INTEGER);
```
# INSERÇÃO DE VALORES EM TABELAS
```
	 sqlite> insert into memos values('deliver project description', 10);
```
```
	 sqlite> insert into memos values('lunch with Christine', 100);
```
# EXIBIÇÃO DE DADOS DE TABELAS
```
	 sqlite> select * from memos;
```
