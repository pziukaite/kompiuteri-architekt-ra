# AN/UYK-44 vs. Intel i960 kompiuterių architektūrų palyginimas

## 1. Įvadas
Trumpas darbo pristatymas, tikslas

## 2. AN/UYK-44 architektūra
### 2.1 Bazinės ir fizinės savybės (2 klausimas)
Tai yra 16 bitų minikompiuteris, buvo sukurtas naudojant integrinius laidynus (LSI/TTL), o ne lempas kaip anksčiau. Atminčiai naudojama magnetinės šerdys (lėtesnis ciklas) ir puslaininkai (greitesnis ciklas). Fiziškai ši architektūra yra pritaikyta standartiniam 19 colių rack'ui(???), tačiau yra lengvesnis ir naudoja mažiau energijos. Dėl to puikiai ttinka naudojimui laivuose (taip ir buvo dažniausiai naudojamas) dėl svorio ir galios kompromiso.
### 2.2 Architektūros tipas (3 klausimas)
AN/UYK-44 yra registrinė CISC tipo architektūra. Programos pagrinde dirba su 16 bendrosios pakirties registrų rinkiniu, o atmintis pasiekiama per „page adress registers", kurie veikia kaip baziniai adresai. turi sdu atskirus registrų rinkinius naudojamus užduočių (task) arba vykdomajam (executive) režimuose. Tai yra registrų architektūra su stipria atminties žemėlapiavimo ir apsaugos posisteme.
### 2.3 Adresų skaičius (4 klasuimas)
Naudojami keli instrukcijų formatai, tačiau daugeliu atvejų - vieno adreso mašina su numatytuoju registru. Elementari matematinė komanda ima vieną operandą iš registro, o kitą iš atminties. Čia rezultatas yra gražinamas į tą patį registrą. Tačiau yra ir opracijų, kurios dirba tik su reistrais ar sisteminių instrukcijų, kurių operandai yra užkoduoti netiesiogiai. Dėl to negalima tiksliai klasifikuoti kaip vieno, dviejų ar trijų adresų schemai. Tiksliausia apibūdinimas - vieno adreso architektūra su numatytuoju akumuliatoriumi.
### 2.4 Registrai (5 klausimas)
Sistema turi mano jau minėtus 16 bitų bendrosios paskirties registrų užduočių režimui ir atskirą rinkinį su tiek  pat registrų vykdomajam režimui. Taip pat, yra 16 bitų programos skaitliukas (P), du 16 bitų būsdnos registrai (SR1 ir SR2), specialūs pertraukimo registrai ir kiti specializuoti registrai. „Page adress registers" yra sudaryti iš keturių rinkinių 64 šešiolikos bitų registrus - jie apibrėžia, kur RAM yra fiksuojami (žemėlapiuojami) konkretūs loginių puslapių numeriai. Ši architektūra turi ir bendrosios paskirties, ir aiškiai specializuotus registrus, kurie yra skirti apsaugai, pertraukimų valdymui ir t.t.
### 2.5 Požymių bitai (6 klausimas)
Aritmetinės ir loginės instrukcijos atnaujina standartinius „flag'us" tokius kaip nulio rezultatą, pernešimą, perpildymą, neigiamą ženklą. Jie vėliau yra naudojami sąlyginiams šuoliams. Kiti bitai nurodo kuriuo iš dviejų režimų yra dirba procesorius, nurodo ar yra leidžiami pertraukimai, valdo prieigą prie „Page adress registers". 
### 2.6 Duomenų plotis (7 klausimas)
Pagrindinis mašininis kodas yra 16 bitų. Visi bendrosios paskirties registrai taip pat yra to paties pločio, atmintis organizuojama 16 bitų žodžiais, kaip ir dauguma instrukcijų. Adresai talpinami 16 bitų vardų erdvėje. Taigi, beveik visais atvejais duomenų plotis šioje architektūroje yra 16 bitų.
### 2.7 Atminties išdėstymas ir adresų erdvė (8 klausimas)
AN/UYK-44 naudoja „paged memory system" modelį. Užduočių režime programa mato 64 loginius puslapius („pages") po 1024 žodžius, todėl efektyvi vardų erdvė yra 64K 16 bitų žodžių. Kiekvienam loginiam puslapiui atitinkame puslapių adresų registre nurodoma, į kurį RAM ar branduolinį atminties puslapį jis bus fiksuojamas. 
### 2.8 Virtuali atmintis (9 klausimas)
Ši sistema nėra sukurta kaip virtualios atminties mašinia, tačiau jos puslapių žemėlapiavimo mechanizmas elgiasi panašiai kaip paprasta virtualioji atmintis apsauginiu aspektu. Loginiai 16 bitų adresai yra verčiami į fizinius per puslapių adresų registrus, o vykdomasis režimas gali juos perrašyti, taip perjungia, kokias atminties sritis mato konkreti užduotis. Taip skirtingi procesai gali būti izoliuoti, o I/O aparatūra gali dirbti su savo buferiais, nematydama kitų duomenų. trūksta tik automatinio puslapių iškėlimo į diską ir atgal, nes viskas turi tilpti pagrindinėje atmintyje (tai yra realaus laiko kontroleris).
### 2.9 Komandų sistema ISA (10 klausimas)
Architektūros komandų sistema yra programuota CISC tipo ISA su dvejais pogrupiais - nepriviligijuotomis ir privilegijuotomis instrukcijomis. 

Nepriviligijuotos instrukcijos apima sveikųjų skaičių aritmetiką (tokias kaip sudėtis, atimtis, daugyba, dalyba), logines opracija (tokias kaip AND, OR, XOR), bitų poslinkius ar rotacijas, sąlyginius ir besąlyginius šuolius , registrų ir atminties užkrovimą bei saugojimą. 

Privilegijuotos instrukcijos valdo puslapių adresų registrus, būsenos registrus, laiko skaitiklį, kontroliuoja I/O grandines, paleidžia diagnostines procedūras. Instrukcijų formatai yra grynai registriniai, registras-atmintis - kitaip nei nepriviligijuotose instrukcijose. 
### 2.10 Adresavimo būdai (11 klausimas)
Pagrindinis naudojamas adresavimo būdas - puslapio numeris + poslinkis, kur puslapio numeris per puslapi7 registrus „išverčiamas" į fizinį bazinį adresą. Instrukcijos gali naudoti registrų adresavimą, netiesioginį adresavimą per žodį atmintyje, santykinį adresavimą šuoliams (nuo P registro) ir specialų adresavimą I/O komandose, kai adresas interpretuojamas kaip nuoroda į I/O kanalų duomenų struktūras. 
### 2.11 I/O galimybės (12 klausimas)
Architektūra yra paremta atskiru įvesties-išvesties valdikliu IOC ir „chain" programomis atmintyje. CPU per priviligijuotas instrukcija sukuria ir paleidžia grandines („chain" programas), kuriose aprašyta, iš kokių puslapių ir į kokius adresus IOC turi skaityti ar rašyti duomenis, kokias išorines funkcija kviesti,, kokius pertraukimus generuoti baigus darbą. Pats IOC yra prijungtas prie standartizuotos karinės magistralės, kuris palaiko įvairius radarus, sencorius, ryšio įrangą ir ginklus, gali pasiekti savo puslapių adresų registrų rinkinius (taip naudojama atskiros atminties sritys). Vėliau Unix STREAMS pagrindu sukurtas veikiantis IOC emuliatorius leido Unix programoms bendradarbiauti su šia architektūra lyg tai būtų įprastas failas - tai suteikė labai lankstų I/O programavimą.
### 2.12 Pertraukimai (13 klausimas)
Architektūra pilnai palaiko pertraukimus. I/O valdiklis IOC generuoja išorinius pertraukimus, kai baigia sekas, aptinka klaidas ar gauna specialius signalus. Šiuos pertraukimus aptinka CPU. CPU išsaugo esamą P ir būsenos registrų reikšmes ir perjungia vykdomojo režimo pertraukimo tvarkyklę. Taip pat, yra programinių pertraukimų bei klaidų („traps"), kurie yra naudojami diagnostikai ir apsaugos pažeidimų fiksavimui (pvz. kai bandoma rašyti į uždraustą puslapį). Pertraukimų tvarkymas yra glaudžiai susijęs su puslapių registrų rinkinių perjungimu, kad tvarkyklė dirbtų savo atskiroje adresų erdvėje ir nesumaišytų vartotojo duomenų.
### 2.13 Duomenų tipai aparatūriniame lygyje (14 klausimas)
Aparatūriniame lygyje architektūra dirba su 16 bitų sveikaisiais skaičiais. Instrukcijos palaiko loginę analizę ir bitų operacijas šiems 16 bitų žodžiams. 
### 2.14 Greitaveika ir kainos/našumo santykis (15 klausimas)
AN/UYK-44 našumas yra maždaug 1 MIPS klasės, tačiau yra žymiai didesnis nei jo protėvio (AN/UYK-20). Puslaidininkės atminties moduliai su 350-450 ns ciklais užtikrina pakankamai greitą prieigą realaus laiko valdymo užduotims, o modulinis dizainas leidžia pridėti daugiau atminties ar I/O kanalų pagal poreikį. Dėk standartizavimo laivyne šią vieną architektūrą galima naudoti daugelyje skirtingų sistemų - taip yra gerinamas bendras kainos ir našumo santykis per visą ekspoatacijos laiką, net jeigu pats aparatas nėra pigus. Dėl savo mažo svorio ir energijos sąnaudų taip pat buvo vienas iš optimalių variantų sistemoms, kuriose buvo svarbi fizinė erdvė ir aušinimo galimybės.
### 2.15 Spartinančioji atmintis (16 klausimas)
Kitaip nei didesniuose „mainframe" tipo kompiuteriuose, šios architektūros aprašymuose spartinančioji atmintis yra beveik neminima. Pagrindinis našumo rezervas čia yra greitesnė puslaidininkė RAM ir efektyvus puslapių žemėlapiavimas bei pertraukimų apdorojimas. Dėl to galima sakyti, jog ši architektūra praktiškai naudoja tik „plokščią" pagrindinę atmintį.
### 2.16 Taikymo sritys (17 klausimas)
Architektūra buvo sukurta kaip universalus ir nedidelis laivų ir kitų gynybinių sistemų kompiuteris. Jis buvo montuojamas povandeniniuose laivuose, pavienių radarų ir sonarų valdymo postuose, raketų paleidimo ir kontrolės sistemose. Konkretus pavyzdys - ši architektūra, valdanti vieną radarų stotį. Per I/O magistralę priima žalius signalų duomenis, juos apdoroja realiu laiku, filtruoja triukšmą, formuoja taikinių sąrašus ir perduoda juos aukštesnio lygio taktinei sistemai ar žmogaus operatoriaus konsolėms.
### 2.17 Programinė įranga ir programavimo įrankiai (18 klausimas)
AN/UYK-44 atsirado, kai laivyno programinė ekosistema buvo gerai išvystyta, todėl jai buvo parašyta daug programinės įrangos. Pagrindinės kalbos - CMS-2 (tradicinė laivyn oaukšto lygio kalba taktinėms sistemoms) ir Ada. Egzistavo specialūs Ada kompiliatoriai, kurie generavo kodą šiai architektūrai, dažnai naudojant VAX ar kitus „mainframes" kaip „host" kompiliavimo platformą. Žemesniame lygyje buvo naudojami surinkėjai, diagnostikos monitoriai, testavimo ir profiliavimo įrankiai, skirti realaus laiko užduotims ir I/O grandinėms tikrinti. 

## 3. Intel i960 architektūra
### 3.1 Bazinės ir fizinės savybės (2 klausimas)
Intel i960 yra vieno lusto CMOS VLSI (didelio integracijos laipsnio) procesorius. i960CA ir i960MX yra pilni 32 bitų RISC procesoriai viename luste. Jie yra skirti įterptoms sistemoms ir avionikai, todėl yra optimizuoti naudoti gan mažai energijos (lyginant su to meto bendros paskirties CPU). Taigi, tai yra tipinė VLSI integrinių grandynų architektūra.
### 3.2 Architektūros tipas (3 klausimas)
Tai yra registrinė „load/store" RISC architektūra. Komandos dirba su registrų failu, o prie atminties kreipiamasi tik specialiomis „load/store" tipo instrukcijomis. Architektūra nenaudoja klasikinio akumuliatoriaus kaip vienintelio rezultatų registro - tai nėra nei akumuliatorinė, nei atmintis į atmintį architektūra. Tačiau architektūros branduolys yra artimas Berklio RISC modeliui - daug registrų, registrų langai procedūrų iškvietimams ir paprasti adresavimo režimai.
### 3.3 Adresų skaičius (4 klasuimas)
Instrukcijų lygmuo yra artimiausias 2-3 adresų registrinei mašinai. Aritmetinės ir loginės instrukcijos naudoja du šaltinius ir vieną paskirties registrą (pvz. addi r1, r2, r3 - du operandai + vienas rezultato registras). Yra formų, kur vienas iš operandų yra „immediate", arba rezultatas rašomas atgal į tą patį registrą, dėl to dalis komandų elgiasi kaip dviejų adresų instrukcijos. Taigi, adresai į atmintį instrukcijose dažniausiai reiškia tik vieną atminties operandą, kitas operandas ir rezultatas - registruose.
### 3.4 Registrai (5 klausimas)
i960 branduolys turi 32 bendrosios paskirties 32 bitų registrus, suskirstytus į 16 globalių (g0-g15) ir 16 lokalių(r0-r15) esamam procedūros „langui".
Superskaliariniame i960CA yra ir „register cache", kur yra laikomi keli paskutinių procedūrų lokalių registrų rinkiniai - iškvietimas/grįžimas praktiškai tik perjungia langą, o ne kopijuoja duomenis. Taip pat, yra specialios pasirties registrai - instrukcijų rodyklė (IP), procesų valdymo (PC), aritmetikos valdymo (AC), įvairūs valdymo ir būsenos registrai ir kt.. Išplėstoje architektūroje papildomai yra registrai, kurie yra susiję su objektų ir puslapių adresavimu, apsauga.
### 3.5 Požymių bitai (6 klausimas)
Pagrindiniai požymaii yra laikomi AC („Arithmetic Controls") registre. Čia yra neigiamumo, nulio, pernešimo, papildymo ir kiti aritmetikos ar lyginimos rezultatus atspindintys bitai. Šie požymiai yra naudojami sąlyginiams šuoliams ir testavimo instrukcijoms. 
### 3.6 Duomenų plotis (7 klausimas)
Bazinė architektūra yra 32 bitų. Registrai ir mašininis kodas - 32 bitai,  adresų erdvė - plokščia 32 bit7. Išplėstinėje architektūroje (ją realizuoja i960MX) atminties posistemė yra 32 bitų - prie kiekvieno 32 bitų žodžio pridedamas žymės („tag") bitas, kuris yra naudojamas apsaugai ir objektų tipams atskirti.
### 3.7 Atminties išdėstymas ir adresų erdvė (8 klausimas)
i960CA turi plokščią 32 bitų adresų erdvę be segmentavimo, tačiau su baitų, žodžių ir žodžių eilės adresavimu, vidine instrukcijų talpykla. Išplėstinėje architektūroje adresavimas tampa objektinis - logišką adresą sudaro objekto  identifikatorius ir poslinkis, o MMU verčia juos į fizinę atmintį, naudodama lenteles ir 33-iajį bitą apsaugai. Taigi, MMU modelis rodo, kad i960 MMU turi aiškiai atskirtas lenteles puslapiams, objektams, valdo prieigos teises ir generuoja apsaugos klaidas. Dėl to atmintes erdvė yra gerai suskaidyta į puslapius ir saugomus objektus, o programavimo lygmeniu OS gali pateikti vientisą virtualią erdvę.
### 3.8 Virtuali atmintis (9 klausimas)
„Protected" ir dar labiau „extended" i960 architektūros lygiai turi pilną virtualiosios atminties palaikymą, kuris yra realizuojamas MMU su puslapiavimo ir objektine apsauga. „extended" architektūroje kiekvienas žodis turi žymės bitą.
### 3.9 Komandų sistema (10 klausimas)
i960 ISA - yra RISC tipo, fiksuoto 32 bitų ilgio instrukcijos, suskirstytos į kelias klases - duomenų perkėlimo („load/store/move"), aritmetikos (addi, subo, muli), loginės (and, or, xor), bitų ir bitų laukų, baitų operacijų, palyginimo (cmpi, cmpo, cmpdeci), šakų (b, bx, bal, „compare and branch"), procedūrų valdymo (call, callx, ret), sisteminių (sysctl1), atominių ir derinimo instrukcijų. 
### 3.10 Adresavimo būdai (11 klausimas)
Pagal oficialų vadovą i960 palaiko kelis klasikinius adresavimo režimus - absoliutų (tiesioginis adresas), registro netiesioginį, indeksuotą su poslinkiu (registras + literalo poslinkis), IP su poslinkiu (instrukcijos rodyklės santykinis adresavimas) ir įvairias „immediate" formas. Bitų ir jų laukų instrukcijos leidžia adresuoti konkrečius bitus/bitų laukus žodyje. 
### 3.11 I/O galimybės (12 klausimas)
Ši architektūra yra orientuota į atmintimi žemėlapiuotą I/O - išorinių įrenginių registrai tiesiog įdedami į adresų erdvę ir yra pasiekiami per įprastas „load/store" instrukcijas. i960 turi integruotus pertraukimų valdiklius, laikmačius.
### 3.12 Pertraukimai (13 klausimas)
Yra gan plati pertraukimų sistema. Pvz. 80960MC varianto duomenyse minima iki 256 pertraukimų vektorių ir iki 32 prioriteto lygių, su vektorine pertraukų lentele ir greitu konteksto perjungimu.
### 3.13 Duomenų tipai aparatūriniame lygyje (14 klausimas)
Pagal i960 CA/CF vadovą aparatūrinė įranga palaiko sveikuosius skaičius, bitus ir bitų laukus, baitų ir žodžių operacija. Branduolinėje architektūroje fiksuoto kablelio aritmetika yra pagrindinė. „Extended" architektūroje atsiranda naujas tipas - objekto/rodyklės žodis su „tag" bitu, kuris atskiria duomenis nuo apsaugotų nuorodų.
### 3.14 Greitaveika ir kainos/našumo santykis (15 klausimas)
i960CA yra pirmasis vieno lusto superskalarus RISC procesorius su 33MHz dažniu ir iki maždaug 66 MIPS našumu, nes vienu metu gali vyskdyti iki dviejų nepriklausomų instrukcijų per vieną ciklą. Taip pat, pasiūlė praktinį superskalarumą įterptoms sistemoms už gan nedidelę kainą (lyginant su to meto dideliais RISC procesoriais).
### 3.15 Spartinančioji atmintis (16 klausimas)
Šio procesoriaus superskalarūs variantai tui „on-chip" spartinančią atmintį. i960CA turi vieną KB instrukcijų „cache", o i960CF - 4 KB instrukcijų ir vieną KB duomenų „cache", dvipusio asociatyvumo, organizuotą žodžių eilėmis, optimizuotą nuosekliam instrukcijų srautui. 
### 3.16 Taikymo sritys (17 klausimas)
i960 šeima buvo plačiai naudota įterptose sistemose - spausdintuvuose, tinklo valdikliuose, terminaluose, modemų įrangoje, tačiau svarbiausios taikymo sritys - anvionikos ir karinės sistemos.
### 3.17 Programinė įranga ir programavimo įrankiai (18 klausimas)
Šiai architektūrai buvo sukurta nemažai programinės įrangos ir kūrimo įrankių. Buvo siūlyti C ir Ada kompiliatoriai, asembleriai, derintuvai ir profiliuotojai. 

## 4. Lyginimas
### 4.1 Panašumai
Ta pati integrinių grandynų era - jos yra realizuotos kaip VLSI/LSI lustao ar modulinės plokštės su puslaidininke atmintimi, be senos elementinės bazės.

Registrinės architektūros  - programos dirba per registrus, o atmintis pasiekiama specialiomis komandomis.

Atiminties valdymo ir apsaugos aparatūrinė sistema - aparatūrinė įranga suskirsto adresų erdvę (puslapiai/objektai), tikrinamos prieigos teisės, leidžia OS izoliuoti skirtingas užduotis.

Pertraukimai - abi buvo kurtos realaus laiko sistemoms (gynuba, avionika). Dėl to abi turi išvystytą pertraukimų sistemą, greitą kontekto perjugimą, atskirus režimus.

### 4.2 Skirtumai
CISC minikompiuteris AN/UYK-44 turi „istorinius" instrukcijų formatus ir yra orientuota į laivyno taktikos sistemas, o RISC superskalaras Intel i960 turi fiksuoto ilgio instrukcijas, „load/store" modelį, tai yra akademinių RISC idėjų ir pramonės standartų mišinys.

UYK-44 žodis yra 16 bitų, o i960 - pilna 32 bitų architektūra, „extended" versija turi dar ir 33-iąjį „tag" bitą.

Pirmoji architektūra yra puslapiuotas 16 adresų modelis, tuo tarpu i960 turi pilną MMU su puslapiavimu/objektais.

i960 yra kur kas stipresnis iš našumo pusės (apie 66 MIPS), o UYK-44 tik 1 MIPS.

UYK-44 yra stipriai orientuota į karinių sistemų I/O, o i960 - universalesnis, įterptinis CPU, dažnai su žemėlapiuojamu I/O.

UYK-44 paskirtis yra gan siauria - daugiausia naudojama JAV laivyne ir gynyboje. i960 irgi yra naudojamas karinėje ir avionikos technikoje, tačiau be to dar plačiai naudojamas komercinėse įterptinėse sistemose (pvz. spausdintuvai).

## 5. Išvados
Taigi, abi architektūros atspindi skirtingas eras - UYK-44 atstovauja senesnės kartos karinio minikompiuterio logiką su 16 bitų CISC, o i960 - šiuolaikinį, 32 bitų RISC. 

Taip pat, abi architejtūros yra projektuotos konkrečioms sistemoms, tačiau skirtingai realizuotos. 

## 6. Naudoti šaltiniai

