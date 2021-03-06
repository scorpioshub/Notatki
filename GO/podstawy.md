
# Sciąga z GO

## zmienne śrowiskowe

```shell
go env
```

### GOPATH

Lokazlizacja kodow GO , workspace wszystkich projektow  
Tam są SRC PKG i BIN  

Create an OS X executable:  
GOOS=darwin GOARCH=386 go build  

Create a Windows executable:  
GOOS=windows GOARCH=386 go build  

Create a Linux executable:  
GOOS=linux GOARCH=arm GOARM=7 go build  

## Pakiety

Pakiety są: executably (tylko main) i library (np fmt). Tych library nie moza uruchomić, można tylko zaimporotwać  
Wszystkie pliki pakietu musza byc  w tym samych jednym foderze i miec package ... name ten sam  
Import własnych pakietów musi być podan wg scieżki gopath, czyli od folderu src.  
Np. D:\GoCode\src\github.com\wysockilukas\misAPI  
Praktyka jest nazywac pakiet tak jak folder, w ktorym jest kod  
Jeśli cos z pakietu jest zadeklarowane z duzej litery to moze byc eksportowane, czyli widoczne dla innych moduow ktory go impotują  

## GO DOC

To narzędzie do twozenia dokumentacji z komentarzy  
Musimy zacząć komentraz od nazy deklaraci np. Package main, main function  
Polecenie poniezej zwraca kometraz do funckji Println z pakietu fmt  

```shell
god doc -src ftm Println
godoc -http=:6060
```

<https://godoc.org/golang.org/x/tools/cmd/godoc>  

## Zmienne i typy danych

```Go
var (
    ToBe   bool       = false
    MaxInt uint64     = 1<<64 - 1
    z      complex128 = cmplx.Sqrt(-5 + 12i)
)
var x, y int = 3, 4
var f float64 = math.Sqrt(float64(x*x + y*y))
int(3.2)  //konwersja
3/2 = 1
3.0/2 = 1.5
```

ale do konwersji z do string jest pakiet strconv  
typ byte = unit8  
rune = int32  

## Strings

String literal to tekst w ""  
Raw string literal to tekst w `` , moze zawierac wiele linii  
String skalda sie z run, ktore sa z bajtow. I niektore run moga miec wiecej niz jeden bajt, a funkcja len - zwraca liczbe bajtow  
Pakiet unicode/utf8, zawiera funckje ktorazwraca liczbe znakow, nie bajtow **utf8.RuneCountInString**  
Pakiet strings, zawiera wiele funckji do string, jak np repeat  
rune to alias typu int32  
String to byte slices lub int32 slices  
'h' - rune litera  
'h' = 104  
'h' = 0x68 (Hex)  
rune code moze przechowac 4 bajty, rune to inczaj unicode costam  
emoji mają kody ok 128557  

string to read only byte slice  
ale moze byc konwertowany na byte i wtdy mizna go modyfikowac np
mozna tez konwertowac string na []rune i wtedy łatwo się czyta znaki w pętli  

```Go
b:=65
string(b) = "A"
b := 65
fmt.Printf("%-10c %-10[1]d\n", b)

str := "Abc"
bytes := []byte(str)
bytes[0] = 'Z'
fmt.Printf("%s\n", bytes)
```

## Maps and Internals

Mapa to key value  
Kolejnosć petli po mapie jest losowa  

```Go
var dict map[string]string    //z jakiegoś powodu te dwie linie daje się razem
dict =make(map[string]string)  //inicjalizacja mapy

len(dict)
value := dict[key]
dict: map[string]string{
    "klucz":"wartość",
}
value, ok := dict[key] //ok is true or false
for k, v := range dict {
}
dict :=make(map[string]string)
delete(dict, "key")
dict = nil
```

## Pętla

```Go
for i := 0; i < 10; i++ {
    sum += i
}
for sum < 1000; {
    sum += sum
}
for {
}
//break, continue
for _, v :=range os.Args[1:] {
}

jakisLabel:
for _, v :=range os.Args[1:] {
    break jakisLabel
}
```

## IF, Switch

Operatory  
&&, ||  !, !=
Dla switch jest cos takiego jak **fallthrough** - pzrechodzi do kolejnego casa  

```Go
switch os := runtime.GOOS; os {  //short switch, zasięg os jest wewnątrz switch  
case "darwin":
    fmt.Println("OS X.")
case "linux":
    fmt.Println("Linux.")
default:
    // freebsd, openbsd,
    // plan9, windows...
    fmt.Printf("%s.\n", os)
}

switch time.Saturday {
case today + 0:
    fmt.Println("Today.")
case today + 1:
    fmt.Println("Tomorrow.")
case today + 2:
    fmt.Println("In two days.")
default:
    fmt.Println("Too far away.")
}

switch {
case t.Hour() < 12:
    fmt.Println("Good morning!")
case t.Hour() < 17:
    fmt.Println("Good afternoon.")
default:
    fmt.Println("Good evening.")
}

switch {
case i > 100

case i > 0:
    //to sie  wykona dla (0,100>
default:

}
```

## Pointers

```Go
i, j := 42, 2701

p := &i         // to pointer do i - przechowuje adres i w pamięci
fmt.Println(*p) // *p to wartosc jaka jest pod adresem na ktory wskazuje p
*p = 21         // zmieniamy wartosc i, pzrez modyfikacje wartosic bezpośrednio wpamieci, gdzie wskazuje pointer p
fmt.Println(i)  // see the new value of i
```

## Struct

```Go
type Vertex struct {
    X int
    Y int
}
v := Vertex{1, 2}
v.X = 4
fmt.Println(Vertex{1, 2})
p := &v
p.X = 100
p  = &Vertex{1, 2} // p jest pointerem i ma typ *Vertex
```

## Slices

Slices nie można porownać  
slicable[ start : stop ]  ; start to index, stop - element positon  
[]byte{'h','e','l','l','o'}[0:1] = 'h'
[]byte{'h','e','l','l','o'}[0:2] = 'h','e'
Slice to struct ktory ma pointer do tablicy, dlugosc i capacity  

```Go
var s []string
b:= []string{"a","b"}
s = append(s, b... )
s = append(s,"c","d","e")
len(a)
sort.Ints([]int{4,2,3,6,8})

make([]int , lenght, capacity)
s:=make([]int, 0, 5)
copy(destSlice, sourceSlice)
```
