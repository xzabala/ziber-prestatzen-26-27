# RA10. IT/OT integrazioa - Ariketa 3: PLCaren enumerazioa eta esplotazioa simulatu

## Helburua
OT ingurune batean PLC baten existentzia eta ezaugarriak aurkitzea, eta sareko segmentazio faltaren ondorioak ulertzea, beti ere laborategi isolatuan eta baimenarekin egiten dena.

## Kontzeptu teorikoak
- PLC baten identifikazioa
- Modbus TCP protokoloa
- Coils eta holding registers
- Nmap NSE script-ak
- Enumerazioa eta eskaneatzea
- SCADA/ICS sistemen segurtasun-arazoak
- Eraso baten ondorioak eta haien efektu fisikoa
- Segurtasun-neurri preemptiboak
- Laburpen eta dokumentazio etikoa

## Ariketa gidatua
### 1. Laborategia prestatu
- Erabili ingurune isolatua eta kontrolatua.
- Beharrezkoa da PLC simulatu bat edo prozesu industrialaren konfigurazio parte bat izatea.
- Ziurtatu azterketa egiteko baimena duzula eta ez duzula kanpoko sistemei eragin.

### 2. Sareko aurkikuntza egin
- Erabili Nmap bezalako tresnak sarean dagoen zerbitzaria edo PLCa aurkitzeko.
- Bilatu protokolo lagungarriak, adibidez Modbus.
- Egin eskaneoa ezarritako sare barruan, eta dokumentatu emaitzak.

### 3. PLCaren ezaugarriak identifikatu
- Bilatu zer zerbitzu dauden zabalik.
- Identifikatu, ahal bada, PLCaren IP, portuak eta protokoloa.
- Dokumentatu zer informazio lortzen den eta zer arrisku dakarten.

### 4. Modbus erregistroak aztertu
- Ikusi zein erregistro mota daude eskuragarri:
  - coils
  - holding registers
- Bilatu nola irakur daitezkeen eta nola alda daitezkeen balioak.
- Garrantzitsua da ezagutzea nola funtzionatzen duen kontrol-sistema industrial baten memoria logikoa.

### 5. Aldaketak simulatu
- Erabili tresna sinpleak edo script-ak balio bat aldatzeko, beti ere laborategi barruan.
- Adibidez:
  - ponparen egoera aldatzea
  - ur-mailaren balio finkoa aldatzea
  - alarma bat aktibatzea edo desaktibatzea
- Behatu nola eragiten duen aldaketa prozesuaren portaeran.

### 6. Ondorioak lotu kontrol-funtzioarekin
- Aztertu zein izan zen eragin fisikoa edo operatiboa aldaketak egin ondoren.
- Idatzi zer gertatuko litzatekeen sare-segmentazioa ez badagoen kasuan.
- Erantsi emaitzak, pantaila-kaptura edo log-ak, balioztatzearekin batera.

### 7. Neurri aurreztzaileak proposatu
- Idatzi segurtasun-neurri nagusiak:
  - sare-segmentazioa
  - bezero/zerbitzari komunikazioaren murrizketa
  - sarrerako baimen mugatua
  - monitorizazioa eta alertak
  - aldaketak erregistratzea

### 8. Amaitzeko erronka
- Sortu laburpen bat: zer gertatu zen, nola antzeman zen eta zer neurriri eman beharko litzaiokeen lehentasuna.
- Eman proposamena ikasle guztientzako defentsa-neurri orokor batzuen bidez.
