# Definició d'adreçament amb classe

A continuació es pot veure l'adreçament de xarxa amb classe resumit.

|Classe|Adreça<br>inicial|Adreça<br>final|Màscara<br>subxarxa|
|----|:----:|:----:|:----:|
|**Class A**|**```0.0.0.0```**|**```127.255.255.255```**|**```/8```**|
|**Class B**|**```128.0.0.0```**|**```191.255.255.255```**|**```/16```**|
|**Class C**|**```192.0.0.0```**|**```223.255.255.255```**|**```/24```**|

I a la següent taula es pot veure l'adreçament de xarxa amb classe, l'espai d'adreces IPv4 de 32 bits es va dividir en 5 classes (A-E).
ND

|Classe|Bits principals|Mida del<br>camp (1)|Mida del<br>camp (2)|Nombre de<br>xarxes|Adreces<br>per xarxa|Adreces totals (3)|Adreça inicial|Adreça final|Màscara de subxarxa (4)|Notació CIDR|
|----|----|----|----|----|----|----|----|----|----|----|
|**Class A**|**```0```**|**```8```**|**```24```**|**```128 (27)```**|**```16,777,216 (224)```**|**```2,147,483,648 (231)```**|**```0.0.0.0```**|**```127.255.255.255[a]```**|**```255.0.0.0```**|**```/8```**|
|**Class B**|**```10```**|**```16```**|**```16```**|**```16,384 (214)```**|**```65,536 (216)```**|**```1,073,741,824 (230)```**|**```128.0.0.0```**|**```191.255.255.255```**|**```255.255.0.0```**|**```/16```**|
|**Class C**|**```110```**|**```24```**|**```8```**|**```2,097,152 (221)```**|**```256 (28)```**|**```536,870,912 (229)```**|**```192.0.0.0```**|**```223.255.255.255```**|**```255.255.255.0```**|**```/24```**|
|**Class D<br>(multicast)**||**```1110```**|(ND)|(ND)|(ND)|(ND)|**```268,435,456 (228)```**|**```224.0.0.0```**|**```239.255.255.255```**|(ND)|**```/4[7]```**|
|**Class E<br>(reserved)**||**```1111```**|(ND)|(ND)|(ND)|(ND)|**```268,435,456 (228)```**|**```240.0.0.0```**|**```255.255.255.255[b]```**|(ND)|(ND)|

**(1)** Mida del camp de bits del número de xarxa

**(2)** Mida del camp de bits restants

**(3)** Adreces totals a la classe

**(4)** Màscara de subxarxa predeterminada en notació decimal de punts

**(ND)** sense definir

Representació per bits
En la següent representació per bits,

* **```n```** indica un bit utilitzat per a l'**ID de xarxa**.
* **```H```** indica un bit utilitzat per a l'**identificador de l'amfitrió**.
* **```X```** indica un bit sense un propòsit especificat.

```
Class A
  0.  0.  0.  0 = 00000000.00000000.00000000.00000000
127.255.255.255 = 01111111.11111111.11111111.11111111
                  0nnnnnnn.HHHHHHHH.HHHHHHHH.HHHHHHHH

Class B
128.  0.  0.  0 = 10000000.00000000.00000000.00000000
191.255.255.255 = 10111111.11111111.11111111.11111111
                  10nnnnnn.nnnnnnnn.HHHHHHHH.HHHHHHHH

Class C
192.  0.  0.  0 = 11000000.00000000.00000000.00000000
223.255.255.255 = 11011111.11111111.11111111.11111111
                  110nnnnn.nnnnnnnn.nnnnnnnn.HHHHHHHH

Class D
224.  0.  0.  0 = 11100000.00000000.00000000.00000000
239.255.255.255 = 11101111.11111111.11111111.11111111
                  1110XXXX.XXXXXXXX.XXXXXXXX.XXXXXXXX

Class E
240.  0.  0.  0 = 11110000.00000000.00000000.00000000
255.255.255.255 = 11111111.11111111.11111111.11111111
                  1111XXXX.XXXXXXXX.XXXXXXXX.XXXXXXXX
```

Per més informació [Classful addressing definition](https://en.wikipedia.org/wiki/Classful_network#Classful_addressing_definition) 

