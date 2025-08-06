> OBS.: audio perde sons -> tftp  

> Conexão não pesistente.  

---

# REQUEST
Pedido feito ao servidor.  

## Linha de pedido.
* identificador do método (GET, POST etc.)
* URI do recurso (endereço no qual será enviado o pedido: /index.php)
* versõa do protocolo (atualemnte existem 4 (0.9, 1.0, 1.1, 2)
  
## Cabeçalho
> informações adicionais sobre a requisição, servidor responde conforme a requisição.  
* geral
* requisição
* entidade

## Corpo/Mensagem
* Dados da requisição.  

---

# RESPONSE
Resposta do servidor a uma requisição do host.  

> Linha de status.  
* versão do protocolo (utilizado no servidor)
* código numérico de status (nnn <= corresponde ao modo como o pedido foi condicionado dentro do servidor ex: 200, 404 etc.)

## Categorias
> Primeiro digitos define a categoria.  
* 1xx Informational: pedido recebido e em processamento
* 2xx Success: pedido aceito e processado
* 3xx Redirection: ações adicionais precisão ser realizadas para completar o pedido
* 4xx Client-error pedido com informações incorretas ou não pode ser processado
* 5xx ServerError: servidor não conseguiu processar pedido, embora pedido pareça estar correto

### Exemplos  
> OBS.: status do servidor são de cunho semântico, NÃO EXISTE OBRIGAÇÃO NA UTILIZAÇÃO DELES   

* 200 Ok
* 301 Moved Permanently
* 404 Not Found
* 505 Internal ServerError


> Texto associado ao status
* cabeçalho
* corpo

---

# Tempos de Carga do HTTP

## Tempo de carga http 1.0
> 2 x n x RTT + somatório do tempo de transmissão  

### Exemplo HTTP 1.0
```
2 x 150 x 120 + 100
300 x 120 + 100
36000 + 100
36100
```  

## Tempo de carga http 1.1 (sem papeline)
> n x RTT + somatório do tempo de transmissão

### Exemplo HTTP 1.1 (sem papeline)
```
150 x 120 + 100
18000 + 100
18100
```  

## Tempo de carga http 1.1 (com papeline)
> RTT + somatório do tempo de transmissão

### Exemplo HTTP 1.1 (com papeline)
```
120 + 100
130
```  

---

# Referência
[10 Maneiras Para Baixar Seu Site Mais Rápido Segundo o Google - Blog Aldeia](https://aldeia.cc/blog/marketing/10-maneiras-para-deixar-seu-site-mais-rapido-segundo-o-google/)  
