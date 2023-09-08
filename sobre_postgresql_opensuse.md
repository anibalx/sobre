# Site que demonstra como instalar
[PostgreSQL](https://en.opensuse.org/SDB:PostgreSQL)  


# Configuração adicional
```
  nano /var/lib/pgsql/data/pg_hba.conf
```  

## Edição do pg_hba.conf
```
  # host    all             all             127.0.0.1/32            ident
  host    all             all             localhost               trust
```  
Irá permitir o acesso com a seguinte digitação do navegador:  
```
  localhost:<COLOQUE PORTA DE ACESSO AO BANCO>
```
Ex:  
``` 
  localhost:40723
```  

## Instalação do pgadmin4
```
  zypper in pgadmin4
```  
