# Distinção
1. Uso do sistema de arquivos (filesystem) → df
2. Uso real por diretório específico → du

* Size → tamanho total do filesystem  
* Used → espaço utilizado  
* Avail → espaço disponível  
* Use% → percentual usado  
* Mounted on → ponto de montagem  
```
df -h
df -hT
df -h . => para um diretório específico
```  

```
du -sh .
du -h --max-depth=1 | sort -h
```  
