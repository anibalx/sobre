# 01 - Criando e Protegendo sua Conta da AWS #BondeDaAWS
Acesse o site da AWS:  
```
  aws.amazon.com
```  

Acesse o site da AWS, para criar uma conta grátis:  
```
  aws.amazon.com/free
```  

**OBS 1**  
 É necessário um **email** para a criação da conta  

**OBS 2**  
 É necessário um **cartão** (débito ou crédito) para a criação da conta  

**OBS 3**  
 É necessário um **número de telefone** para a criação da conta  

## Após a criação da conta
Acesse a aba de pesquisa e digite:  
```
  IAM # (dashboard)
```  

Procure por MFA (Multi-Factor Authentication) e cofigure-o para
seu usuário root

Após isso, neste mesmo local, procure:  
```
Access Management
  users
```  

Isso permitirá a criação de um novo usuário dentro desta conta,
mas sem que seja **root**

**OBS**  
O usuário root, deve ser protegido, por isso a criação de usuário não root

Dentro da aŕea de configuração de usuário, 
existe a possibilidade de escolha das credenciais de acesso:  
```
  Access Key - Programmatic access          # acesso via programas e scripts
  Passwont - AWS Management Console access  # acesso via interface web
```

Em seguida, escolha as permissões de acesso deste novo usuário:  
```
Attach existing policies directly
  AdministratorAccess
```  

Após a criação deste novo usuário, um link será gerado.  
Veja o exemplo:  
```
  https://826500377201.signin.aws.amazon.com/console
```  

Acesse essa nova conta por meio deste link (veja o exemplo acima),
digite a senha e conecte a conta AWS, sem que seja root  

# 02 - Publicando um Site no S3 #BondeDaAWS
Acesse a aba de pesquisa e digite:  
```
 AMAZON S3
```  

Em AMAZON S3, crie um bucket
```
 AMAZON S3
  Buckets
    Create Buckets
```  
 
 Escolha um nome e uma região.  

 **OBS 1**
Acesse o site abaixo, para identificar a os SEVERS da AWS.  
 ```
 infrastructure.aws
 ```  

 **OBS 2**
Realize um ping da sua máquina para os provedores de datacenters:  
 ```
 cloudping.info
 ```  

**OBS 3**
Ddetalhes importantes para levar em conta a construção de seu bucket:  
- Latência  
- Preço  
- Disponibilidade  
- Complience  
- Sustentabilidade  

**OBS 4**
Sobre segurança, como é um site e se deseja acesso do público,
será desativado:  
```
  Block Public Access settings for this bucket
```

# 03 - Servindo uma Aplicação Web no EC2 #BondeDaAWS
Uso do **EC2**, serviço para disponibilizar aplicação.  

## Zonas de disponibilidades
Conjunto de data centers, isolados.  

Nomeadas por um nome (nome da região) seguido por uma letra.  
> Exemplo: US West (Oregon)
```
    us-west-2a
    us-west-2b
    us-west-2c
```  

**OBS**
Para alta disponibilidade, crie o recurso em mais deuma zona.  

## Inicio de uma aplicação
Entre em **Launch Instance**.  
* Escolha o nome.  

Á direita, em Summary:
* Escolha o número de instâncias.  

Abaixo, em **Quick Start**.
* Escolha a imagem (ISO).  
* Escolha a arquitetura.  

Em **Key Pair**, escolha o par de chaves para acesso remoto.  

# 04 - Desempenho e Armazenamento no EC2 #BondeDaAWS
Fatores de custo na hora de escolher o tipo de instância.  
* CPU
* MEMÒRIA
* EFEMERAL STORAGE 
    1. discos internos já incluídos no preço da instância
    2. Efêmero pois, ao dar stop e star numa instância, a instância terá seu início em outro hardware, com outro storage.
    3. discos internos, discos locais
    4. tamanho fixo
* PERSISTENCE STORAGE 
    1. discos não incluídos no preço da instância (paga-se o extra)
    2. discos esternos, tráfego de rede
    3. tamanho flexível
* ACELERAÇÂO (GPU etc.)
* REDE

```
    US-CAST-IA

        vpc.xxxx ------ zona de disponibilidade                                        EC2
    ┌─────────────────────────────────────────────────────────────────┐
    │                             INSTANCE                            │       │
    │                             1-xxxxxx                            │       │
    │                   ┌───────────────────────────┐                 │       │
    │                   │        ┌─────────┐        │                 │       │      ELASTIC
    │                   │        │   CPU   │        │                 │       │       BLOCK
    │                   │        └─────────┘        │                 │       │      STORAGE
    │                   │        ┌─────────┐        │                 │       │       (EBS)
    │                   │        │ MEMÒRIA │        │                 │       │
    │                   │        └─────────┘        │                 │       │    PERSISTENTE
    │                   │     ESFEMERAL STORAGE     │                 │       │      STORAGE
    │                   │   ┌──────┐      ┌──────┐  │                 │       │      ┌─────┐
    │                   │   │      │      │      │  │                 │       │      │     │
    │                   │   └──────┘      └──────┘  │                 │       │      └─────┘
    │                   │        ACELERAÇÂO         │                 │       │         │
    │                   │  ┌─────┐ ┌────┐ ┌─────┐   │                 │       │         │
    │                   │  │ GPU │ │ HD │ │ GPU │   │                 │       │         │
    │                   │  └─────┘ └────┘ └─────┘   │                 │       │         │
    │                   │           REDE            │                 │       │         │
    │                   │        ┌─────────┐        │                 │       │         │
    │                   │        │         │        │                 │       │         │
    │                   │        └─────────┘        │                 │       │         │
    │                   └─────────────|─────────────┘                 │       │         │
    └─────────────────────────────────|───────────────────────────────┘                 │
                                      └─────────────────────────────────────────────────┘

```
> OBS Optimizer: separa os tráfegos de rede  

# 05 - Criando a sua rede VPC #BondeDaAWS
VPC = Virtual Privace Computer  

# 06 - Criando um Banco de Dados no RDS #BondeDaAWS
Banco MySQL


# REFERÊNCIAS
[01 - Criando e Protegendo sua Conta da AWS #BondeDaAWS](https://vimeo.com/704815762)
[02 - Publicando um Site no S3 #BondeDaAWS](https://vimeo.com/704819849)
[03 - Servindo uma Aplicação Web no EC2 #BondeDaAWS](https://vimeo.com/704824006)
[04 - Desempenho e Armazenamento no EC2 #BondeDaAWS](https://vimeo.com/704830749)
[05 - Criando a sua rede VPC #BondeDaAWS (audio failed)](https://vimeo.com/707515319)
[06 - Criando um Banco de Dados no RDS #BondeDaAWS](https://vimeo.com/704835542)
[07 - Como tirei todas as Cerfiticações da AWS #BondeDaAWS](https://www.youtube.com/watch?v=Zx5GR1AED1w)
