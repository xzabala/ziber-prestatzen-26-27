# RA10. IT/OT integrazioa - Ariketa 1: Prozesu industrialaren simulazioa

## Helburua
Prozesu industrial baten funtzionamendua ulertzea, IT eta OT sistemak nola elkarreragiten duten ikustea eta PLC, SCADA eta HMI bezalako osagaien rola ezagutzea.

## Kontzeptu teorikoak
- IT eta OT arteko desberdintasunak
- PLC (Programmable Logic Controller)
- SCADA sistema
- HMI (Human Machine Interface)
- Modbus TCP
- Ladder logika
- Factory I/O
- OpenPLC
- Prozesu industrialaren errealismoa eta segurtasun funtzionala
- Datuen fluxua kontrolagailu batetik makinara

## Ariketa gidatua
### 1. Ingurunea prestatu
- Instalatu edo prestatu laborategiko makina birtuala.
- Ziurtatu OpenPLC eta Factory I/O martxan daudela.
- Egin segurtasun-murrizketak: lan-eremua isolatua izan behar da eta ez da kanpoko sareetara konektatu behar.

### 2. Sistema nagusiaren arkitektura ezagutu
- Identifikatu zein osagaik osatzen duten sistemaren multzoa:
  - PLCa: prozesua kontrolatzeko arduraduna
  - SCADA: monitorizazio eta kontrol zentralizatua
  - HMI: operadoreari interfaze grafikoa ematen diona
  - Makina/maqueta: fisikoki prozesua eragiten duena
- Idatzi laburki nola komunikatzen diren osagai hauek eta zein protokolo erabiltzen dituzten.

### 3. Prozesu industriala konfiguratu
- Factory I/O-n prozesu sinple bat aukeratu, adibidez ur-tanga edo sarrera/irteera sistema.
- Aukeratu kontrolatzeko funtzio bat, adibidez:
  - ur-maila mantentzea
  - ponpa martxan jartzea edo gelditzea
  - balbula irekitzea edo ixten uztea
- Konfiguratu eremua ahalik eta errealistena izateko.

### 4. PLCa programatu
- OpenPLC-n ingurune berri bat sortu.
- Programazio-lengoaia gisa Ladder erabili.
- Sartu logika sinplea:
  - balioa baxua bada, ponpa aktibatu
  - balioa altua bada, ponpa desaktibatu
  - alarma aktibatu prozesuaren egoera arriskutsuan
- Gorde programa eta probatu.

### 5. SCADA/HMIarekin lotu
- Konfiguratu komunikazioa PLC eta Factory I/Oren artean.
- Egiaztatu SCADA edo HMI panelak prozesuaren egoera irudikatzen duela.
- Gehitu neurri erraz batzuk, adibidez:
  - ur-maila adierazlea
  - alarma aktibazioaren seinalea
  - kontrol-botoi bat ponparen eskuz kontrolatzeko

### 6. Probaren emaitzak dokumentatu
- Egin taula bat egoera normal, alerta eta akats kasuetarako.
- Idatzi zer gertatu zen prozesua martxan jartzerakoan.
- Aztertu zein izan zen kontrolaren erantzun-denbora eta zein faktore eragin zuten.

### 7. Ondorioak atera
- Aztertu nola desberdinak diren IT eta OT sistemak eragiketa-egoeran.
- Idatzi zer behatu duzun prozesuaren kontrolan eta segurtasun-funtzionalaren garrantzia.

### 8. Entregagarri proposatua
- Pantaila-argazki edo irudi bat prozesuaren konfigurazioarekin.
- PLC programaren laburpena.
- Oharrak prozesuaren portaera eta kontrolaren arazoak aztertzeko.
