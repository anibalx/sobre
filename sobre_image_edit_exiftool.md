# Exiftool
> Delete all meta information  
```
exiftool -all= dst.jpg
```  

> Delete all meta information from an image and add a comment back in  
```
exiftool -all= -comment='lonely' dst.jpg
```   

> Delete Photoshop meta information from an image  
```
exiftool -Photoshop:All= dst.jpg
```  

> Extract information from an embedded thumbnail image  
```
exiftool image.jpg -thumbnailimage -b | exiftool -
```  

> Add an IPTC keyword in a pipeline, saving output to a new file  
```
cat a.jpg | exiftool -iptc:keywords+=fantastic - > b.jpg
```  

---

# Mat2
> Show metadados  
```sh
mat2 --show filename.pdf
```  

> Limpe o arquivo  
```sh
mat2 filename.pdf
```  

> Mantém a integridade do arquivo  
```sh
mat2 -L filename.pdf
```  

> Lista os metadados  
```sh
mat2 -s arquivo.png
```  

> Substitui o original pela cópia  
```sh
mat2 --inplace arquivo.pdf
```  

> Limpeza em modo leve  
```sh
mat2 -L arquivo.pdf
```  

> Todos os formatos suportados pelo programa  
```sh
mat2 -l
```  

> Verifica as dependências  
```sh
mat2 --check-dependencies
```  

> Menu de ajuda  
```sh
mat2 -h
```  
