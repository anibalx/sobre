# Chaves
## Privada
Sempre fica com você.  

## Pública
Pode disponibilizar para outras pessoas.  


# GPG 
## < 2.0
```
    gpg --gen-key
```  

# GPG 
## > 2.0
```
    gpg --full-generate-key
```  

## Ask
```
    1. Selecione tipo de chave desejado
    2. Tempo de validade da chave
    3. Informações pessoais
        * Nome
        * email
        * comentário
```  

## Passphrase
Senha de assinatura de criptografia, descriptografia de documentos.  

## Gpg: list keys
```
    gpg --list-keys
    gpg -k
    gpg -K
```  

## GPG: bonita exibição
```
    gpg --fingerprint
```  

## GPG: cerfitificado de revogação
```
    gpg --output revocation.crt --gen-revoke <EMAIL>
    gpg --output revocation.crt --gen-revoke <PUB_ID> # últimos 16 caracteres
```  

## GPG: exportar chave pública
```
    gpg --export --armor <EMAIL> --output <FILE_PUB_KEY>.txt
    gpg --export --armor <PUB_ID> > <FILE_PUB_KEY>.txt
```  

## GPG: exportar chave privada
```
    gpg --export-secret-keys --armor <EMAIL> --output <FILE_PRIVATE_KEY>.txt
    gpg --export-secret-keys --armor <PUB_ID> > <FILE_PRIVATE_KEY>.txt
```  

### GPG: cripografe a chave privada
```
    gpg --symmetric <FILE_PRIVATE_KEY>.txt
```  

Uma vez criptografada, salve em um dispositivo externo.  

### GPG: descripografe a chave privada
```
    gpg --output <NEW_FILE_PRIVATE_KEY>.txt -d <FILE_PRIVATE_KEY>.gpg
```  
