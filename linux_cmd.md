
kopiowanie plikow ktorych nazwa nie zaczyna sie od liczby  
```bash
find . -maxdepth 1 -regex '\./[^0-9].*\.png' -exec cp {} /data/htdocs/mobile/img \;
```
Usuwanie katalogu z zawartoscia  
```bash
rm -rf lite/
```

Kopiowanie folder do folderu  
```bash
cp -avr /data/MIS_OBIEE/disco/SYSTEM/lite/ /data/htdocs/lite/
```