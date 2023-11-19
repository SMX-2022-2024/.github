# Fer consultes a un **Servidor DNS**

A continuació s'estudia una eina per poder conèixer com obtenir la resposta a **consultes DNS** que volem fer.

El propi sistema ja s’encarrega de fer les consultes automàticament al **DNS** quan ho necessita, però també és una eina que es pot utilitzar manualment, per extreure informació molt valuosa d’un domini. Motiu pel que hem d’assegurar una bona higiene del mateix.

L’eina, d’ús més habitual, per fer les consultes a un **servei de DNS** és el **```nslookup```**. És una eina de **la consola de sistema**, per executar-la, cal anar a la consola

<kbd>WIN</kbd> + <kbd>R</kbd>

que ens obrirà la finestra de **```Run```**  i escriure ```cmd```, per què ens obri la **consola de sistema**.

![executar-cmd.png](../images/nslookup-dns-01-cmd.png)

Un cop ja tinguem la **consola de sistema** oberta, hem d'esbrinar quin és el servidor dns que tenim configurat. Per fer-ho cal consultar la configuració de la nostra **interfície de xarxa**. Escriurem **```ipconfig /all```**, per què ens mostri la configuració de **TOTES** les nostres **interfícies de xarxa**.

![Alt text](../images/nslookup-dns-02-ipconfig-all.png)

A la imatge veiem que tenim 3 **interfícies de xarxa**:

|**Nom**|**Adreaça IP**|**Servidor DNS**|
|----|----:|----:|
|**```NAT```**|**```10.0.2.15```**|**```10.0.2.3```**|
|**```XarxaInterna```**|**```172.128.8.1```**|**```8.8.8.8```**<br>**```8.8.4.4```**|
|**```HostOnly```**|**```192.168.56.10```**|**```8.8.8.8```**<br>**```8.8.4.4```**|

Un cop que ja sabem quina és la configuració del **servidor de dns** de les nostres **interfícies de xarxa**, ja podem entrar a l'eina **```nslookup```**.

Des de la línia de comandes executem la comanda **```nslookup```**, i ens obrirà l'entorn d'**```nslookup```** per poder realitzar les consultes que vulguem.

![Alt text](../images/nslookup-dns-03-open-nslookup.png)

Com veiem en el nostre cas, la primera informació que ens apareix és:

```
Default server: UnKnown
Address: 10.0.2.3
```

Això ens indica que en el moment d'iniciar l'aplicació **```nslookup```**, el **servidor de DNS** que té configurat no és un servidor definit com a **servidor de DNS**.

## Canviem el **servidor de DNS** al qual volem fer les consultes.

Per indicar a quin **servidor de DNS** volem fer les consultes, li indiquem de la següent manera:

* **Comanda**

```
server 8.8.8.8
```

* **Sortida**

```
> server 8.8.8.8
Default server: dns.google
Address: 8.8.8.8
```

**Ara sí!**, l'aplicació **```nslookup```** ens indica que el **servidor de DNS** que li hem assignat, amb **adreça ip** **```8.8.8.8```**, **SÍ** que és un **servidor de DNS** correcte.
I a més a més, a part també ens informa de que el **servidor de DNS** amb l'**adreça ip** **```8.8.8.8```** que ha trobat respon al nom **```dns.google```**.

![Alt text](../images/nslookup-dns-04-canvi-servidor.png)

Per tant, a partir d'ara les respostes que rebrem a les **consultes DNS** que fem, seran les respostes que ens retorni  **servidor de DNS** **```dns.google```** amb l'**adreça ip** **```8.8.8.8```**.


## Consulta a un **registre de tipus ```A```**

La primera consulta que farem es tracta d'una consulta a un **registre de tipus ```A```**.

> [!IMPORTANT]
>
> **Registre de tipus ```A```**
> 
> Els **```HOSTS```** (**registres de tipus** **```A```**) que relacionen un nom amb una **adreça IP**.
> Per més informació pot repassar la teoria a [**Teoria de DNS (Domain Name System) ![icona-pdf-30x30.png](https://github.com/SMX-2022-2024/.github/blob/main/profile//images/icona-pdf-30x30.png)**](https://github.com/SMX-2022-2024/.github/blob/main/profile/manuals/smx-mp07-0003-uf01-pres0003-teoria-dns.pdf)


**1.** Consulta **```ginebro.cat```**

Volem coneixer quina és la resposta que ens retorna el servidor **```dns.google (8.8.8.8)```** a la pregunta sobre el servidor **```ginebro.cat```**.

```
> ginebro.cat
Server: dns.google
Address: 8.8.8.8

Non-authoritative answer:
Name:    ginebro.cat
Address: 217.149.11.212
```

Veiem que la resposta a la pregunta de quina adreça ip respon al nom **```ginebro.cat```** és **```217.149.11.212```**

No ens ho ha dit, pero aquesta consulta ha estat de **tipus ```A```**. Per defecte, si no es diu el contrari, les ***consultes DNS*** sempre son a registres de **tipus ```A```**


Important el tipus de resposta que retorna el servidor: ***Non-authoritative answer*** (**Resposta no autoritzada**), si fos autoritzada es podria arribar a "***robar***" totes les adreces que conté el **DNS**, per després utilitzar-ho amb finalitats diguem ***no massa clares***.

**2.** Consulta de **tipus ```soa```** a **```ginebro.cat```**

Per consultar al **servidor DNS**, la informació general del domini com pot ser el servidor DNS que el manté, adreça de contacte, etc. Cal canviar el tipus de consulta:

> Per modificar el tipus de registre que volem realitzar cal fer servir a comanda **```type=```** i el tipus de **registre DNS**.

```
> set type=soa
>
```

Recordem que **```soa```** és el **node superior** d’una zona (**```SOA```**, ***```S```***```tart``` ***```O```***```f``` ***```A```***```uthority```).

```
> ginebro.cat
Server: dns.google
Address: 8.8.8.8

Non-authoritative answer:

ginebro.cat
        primary name server: ns1.filnet.es
        responsible mail addr = mariaexposito.ginebro.cat
        serial  = 2023102906
        refresh = 10800 (3 hours)
        retry   = 3600 (1 hour)
        expire  = 1209600 (14 days)
        default TTL = 10800 (3 hours)
>
```


> [!IMPORTANT]
>
> **3.** Consulta de **tipus ```mx```** a **```ginebro.cat```**
> 
> #### **2.3.** **Registres de tipus** **```MX```**
> 
> Els **serveis especials**, alguns **serveis especials**, com el cas del **servei de correu electrònic** (**```registre MX```**) que relaciona un domini amb el **```HOST```** on s’ha d’**entregar el correu**.
> Per més informació pot repassar la teoria a [**Teoria de DNS (Domain Name System) ![icona-pdf-30x30.png](https://github.com/SMX-2022-2024/.github/blob/main/profile//images/icona-pdf-30x30.png)**](https://github.com/SMX-2022-2024/.github/blob/main/profile/manuals/smx-mp07-0003-uf01-pres0003-teoria-dns.pdf)


Per esbrinar quin és el servidor de correu electrònic d’un domini:

> Per modificar el tipus de registre que volem realitzar cal fer servir a comanda **```type=```** i el tipus de **registre DNS**.

```
> set type=mx
>
```

I sembla que no ha passat res. Però ara si fem la consulta ens tornarà la resposta al registre de **tipus ```mx```** del nom **```ginebro.cat```**


```
> ginebro.cat

Server: dns.google
Address: 8.8.8.8

Non-authoritative answer:
ginebro.cat	    MX preference = 30 aspmx3.googlemail.com
ginebro.cat	    MX preference = 30 aspmx5.googlemail.com
ginebro.cat	    MX preference = 10 aspmx.l.google.com
ginebro.cat	    MX preference = 30 aspmx2.googlemail.com
ginebro.cat	    MX preference = 20 alt2.aspmx.l.google.com
ginebro.cat	    MX preference = 20 alt1.aspmx.l.google.com
ginebro.cat	    MX preference = 30 aspmx4.googlemail.com
```

El resultat que retorna va relacionat per la **preferència ```MX```** i el servidor on enviar el correu.

> La **preferència ```MX```** indica a quin servidor s’ha de preguntar primer, en cas que no respongui, el segon, tercer etc. Com més petit és el número, més preferència té **```10```**, **```20```**, **```30```**, ...

#### **2.2.** **Registres de tipus** **```CNAME```**

> [!IMPORTANT]
>
> **Registre de tipus ```CNAME```**
> 

Els **```SOBRENOMS```** o **àlies**, serien els **registres** **```CNAME```** que relacionen un **sobrenom** a un **nom**


**4.** Consulta de **tipus ```CNAME```** a **```mail.ginebro.cat```**

Per comprovar on apunta un sobrenom (**```CNAME```**):

```
> set type=cname
>
```

```
> mail.ginebro.cat

Server: dns.google
Address: 8.8.8.8

Non-authoritative answer:
mail.ginebro.cat 	    canonical name = ghs.google.com
```

**5.** Consulta de **tipus ```PTR```**

I en el cas que tinguem una **adreça IP** (**```PTR```**) i es vol saber a qui correspon?


```
> set type=ptr
>
```

```
> 217.149.11.212

Server: dns.google
Address: 8.8.8.8

Non-authoritative answer:
212.11.149.217.in-addr.arpa    name = srv11212.servatica.com
```

Per què ens pot ajudar aquesta eina?

* Comprovar que es resolt correctament un nom d’equip quan s’intenta accedir des d’un navegador i indica que no la troba o no existeix.
* Comprovar quins són els servidors de correu electrònic d’un domini, per després fer proves de connectivitat sobre els mateixos.
* Com es resol l’adreça IP i a quin domini pertany, per les comprovacions de reverse lookup de correu electrònic.
* Saber on està allotjat un domini concret.
* etc.

**6.** Consulta de **registres ```DNS```** a [**who.is**](who.is)

Una altra manera de veure aquesta informació és amb pàgines web com [who.is](https://who.is), que retorna la informació de **TOTS** els **registres DNS** que hi ha a **Internet**.

[https://who.is/dns/ginebro.cat](https://who.is/dns/ginebro.cat)


![who-is-dns-ginebro-cat.png](../images/who-is-dns-ginebro-cat.png)

