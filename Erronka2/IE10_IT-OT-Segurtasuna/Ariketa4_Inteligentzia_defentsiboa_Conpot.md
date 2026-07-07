# RA10. IT/OT integrazioa - Ariketa 4: Defentsa-inteligentzia eta Conpot

## Helburua
OT sarean intrusio-saiakera bat detektatzeko ahalmena sortzea, honeypot industrial bat ezarriz eta alertak sortuz.

## Kontzeptu teorikoak
- Honeypot industriala
- Conpot
- Intrusio-detekzioa
- Logen bilketa
- SIEM
- Wazuh
- Elastic
- ICS protokoloak eta beren emulazioa
- Alerten prioritizazioa
- Behaketa eta erantzuna

## Ariketa gidatua
### 1. Helburua eta testuingurua ulertu
- Ikasi zer den honeypot industrial bat eta zergatik erabil daitekeen OT sarean.
- Ulertu honeypota ez dela sistema erreal baten ordezkoa, baizik eta engainatzeko diseinatutako interfazea.
- Ezarri xedea: sarean sarrera-eskaneoa antzematea eta alarma sortzea.

### 2. Conpot instalatu
- Erabili ingurune isolatuan Conpot.
- Konfiguratu PLC edo sistemen emulazioa emateko, adibidez Siemens S7 protokoloa edo antzeko zerbait.
- Ziurtatu zerbitzua martxan dagoela eta atzemandako eskaerak erregistratzen dituela.

### 3. Sarean kokatu
- Jarri Conpot OT sarearen barruan, benetako sistemen gertuagora edo beren segmentu berean.
- Ezarri sarea aplikazioen eta portuen aurkikuntza errazagoa izan dadin.
- Saihestu eta ez utzi benetako kontrol-sisteman eraginik izan.

### 4. Eskaneatzea simulatu
- Erabili makina erasotzaile edo ataka-simulazio bat Conpot-en aurka eskaneoa egitea.
- Abiarazi eskaneoa eta behatu nola erantzuten duen honeypot-ak.
- Dokumentatu eskaneatutako portuak eta konexio motak.

### 5. Logak sortu eta bildu
- Ikusi Conpot-ek sortutako log-ak.
- Bildu informazio garrantzitsua, hala nola IP iturburua, portua eta eskaeraren mota.
- Gorde emaitzak fitxategi batean edo bidali SIEM-era.

### 6. Alertak konfiguratu
- Wazuh edo Elastic erabiliz, arau sinple bat sortu eskaneoa detektatzeko.
- Defini ezazu alerta bat, adibidez:
  - hainbat porta azkar eskaneatzea
  - protokolo industrial bati lotutako eskaera berria
  - etengabeko konexio-saiakera bat
- Probatu alerta martxan dagoela.

### 7. Aztertu emaitzak
- Ikasi nola laguntzen duen detekzio goiztiarra sareko iruzurrarekin.
- Aztertu alerta batek zer informazio eman behar duen operadore batek erantzuteko.
- Idatzi zer neurriri eman beharko litzaioke lehentasuna.

### 8. Entregagarri proposatua
- Honeypot konfigurazioaren deskribapena.
- Log-ak eta alertak erakusten dituzten adibideak.
- Laburpen bat nola lagundu dezakeen defentsa-inteligentziak OT inguruneetan.
