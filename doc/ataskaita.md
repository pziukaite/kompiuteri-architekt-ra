# AN/UYK-44 vs. Intel i960 kompiuterių architektūrų palyginimas

## 1. Įvadas
Trumpas darbo pristatymas, tikslas

## 2. AN/UYK-44 architektūra
### 2.1 Bazinės ir fizinės savybės (2 klausimas)
Tai yra 16 bitų minikompiuteris, buvo sukurtas naudojant integrinius laidynus (LSI/TTL), o ne lempas kaip anksčiau. Atminčiai naudojama magnetinės šerdys (lėtesnis ciklas) ir puslaininkai (greitesnis ciklas). Fiziškai ši architektūra yra pritaikyta standartiniam 19 colių rack'ui(???), tačiau yra lengvesnis ir naudoja mažiau energijos. Dėl to puikiai ttinka naudojimui laivuose (taip ir buvo dažniausiai naudojamas) dėl svorio ir galios kompromiso.
### 2.2 Architektūros tipas (3 klausimas)
AN/UYK-44 yra registrinė CISC tipo architektūra. Programos pagrinde dirba su 16 bendrosios pakirties registrų rinkiniu, o atmintis pasiekiama per puslapių adresų reegistrus, kurie veikia kaip baziniai adresai. turi sdu atskirus registrų rinkinius naudojamus užduočių (task) arba vykdomajam (executive) režimuose. Tai yra registrų architektūra su stipria atminties žemėlapiavimo ir apsaugos posisteme.
### 2.3 Adresų skaičius (4 klasuimas)
Naudojami keli instrukcijų formatai, tačiau daugeliu atvejų - vieno adreso mašina su numatytuoju registru. Elementari matematinė komanda ima vieną operandą iš registro, o kitą iš atminties. Čia rezultatas yra gražinamas į tą patį registrą. Tačiau yra ir opracijų, kurios dirba tik su reistrais ar sisteminių instrukcijų, kurių operandai yra užkoduoti netiesiogiai. Dėl to negalima tiksliai klasifikuoti kaip vieno, dviejų ar trijų adresų schemai. Tiksliausia apibūdinimas - vieno adreso architektūra su numatytuoju akumuliatoriumi.
### 2.4 Registrai (5 klausimas)
Sistema turi mano jau minėtus 16 bitų bendrosios paskirties registrų užduočių režimui ir atskirą rinkinį su tiek  pat registrų vykdomajam režimui. Taip pat, yra 16 bitų programos skaitliukas (P), du 16 bitų būsdnos registrai (SR1 ir SR2), specialūs pertraukimo registrai ir kiti specializuoti registrai. „Page adress registers" yra sudaryti iš keturių rinkinių 64 šešiolikos bitų registrus - jie apibrėžia, kur RAM yra fiksuojami (žemėlapiuojami) konkretūs loginių puslapių numeriai. Ši architektūra turi ir bendrosios paskirties, ir aiškiai specializuotus registrus, kurie yra skirti apsaugai, pertraukimų valdymui ir t.t.
### 2.5 Požymių bitai (6 klausimas)
Aritmetinės ir loginės instrukcijos atnaujina standartinius „flag'us" tokius kaip nulio rezultatą, pernešimą, perpildymą, neigiamą ženklą. Jie vėliau yra naudojami sąlyginiams šuoliams. Kiti bitai nurodo kuriuo iš dviejų režimų yra dirba procesorius, nurodo ar yra leidžiami pertraukimai, valdo prieigą prie „Page adress registers". 
## 2.6 Duomenų plotis (7 klausimas)
### 2.7 Atminties išdėstymas ir adresų plotis (8 klausimas)
### 2.8 Virtuali atmintis (9 klausimas)
### 2.9 Komandų sistema (10 klausimas)
### 2.10 Adresavimo būdai (11 klausimas)
### 2.11 I/O galimybės (12 klausimas)
### 2.12 Pertraukimai (13 klausimas)
### 2.13 Duomenų tipai aparatūriniame lygyje (14 klausimas)
### 2.14 Greitaveika ir kainos/našumo santykis (15 klausimas)
### 2.15 Spartinančioji atmintis (16 klausimas)
### 2.16 Taikymo sritys (17 klausimas)
### 2.17 Programinė įranga ir programavimo įrankiai (18 klausimas)

## 3. Intel i960 architektūra
### 3.1 Bazinės ir fizinės savybės (2 klausimas)
### 3.2 Architektūros tipas (3 klausimas)
### 3.3 Adresų skaičius (4 klasuimas)
### 3.4 Registrai (5 klausimas)
### 3.5 Požymių bitai (6 klausimas)
### 3.6 Duomenų plotis (7 klausimas)
### 3.7 Atminties išdėstymas ir adresų plotis (8 klausimas)
### 3.8 Virtuali atmintis (9 klausimas)
### 3.9 Komandų sistema (10 klausimas)
### 3.10 Adresavimo būdai (11 klausimas)
### 3.11 I/O galimybės (12 klausimas)
### 3.12 Pertraukimai (13 klausimas)
### 3.13 Duomenų tipai aparatūriniame lygyje (14 klausimas)
### 3.14 Greitaveika ir kainos/našumo santykis (15 klausimas)
### 3.15 Spartinančioji atmintis (16 klausimas)
### 3.16 Taikymo sritys (17 klausimas)
### 3.17 Programinė įranga ir programavimo įrankiai (18 klausimas)

## 4. Lyginimas
### 4.1 Panašumai
### 4.2 Skirtumai

## 5. Išvados

## 6. Naudoti šaltiniai
