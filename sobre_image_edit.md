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
