# RA10. IT/OT integrazioa - Ariketa 2: Segmentazioa eta isolamendua

## Helburua
IT eta OT sareen artean muga argi bat ezartzea, eta trafikoa kontrolatzeko politika eraginkorrak aplikatzea malware edo eraso baten hedapena mugatzeko.

## Kontzeptu teorikoak
- Purdue eredua
- IT sare korporala
- OT sare industriala
- Segmentazioa
- DMZ
- Zero Trust
- Firewall politiken arabera trafikoa baimendu/ukatu
- Bastion host edo jump host
- VPN isolatua
- Sareko mugak eta aplikazio kritikoak

## Ariketa gidatua
### 1. Topologia diseinatu
- Marraztu sare-diagrama sinple bat hiru eremurekin:
  - sare korporala (oficina)
  - DMZ edo eremu intermediarioa
  - sare industriala (planta/OT)
- Ezarri nola komunikatuko diren eremu hauek eta zein zerbitzu bakarrik izan behar duten sarbidea.

### 2. Eremuen arteko mugak definitu
- Zehaztu zein zerbitzu edukiko diren sare korporalean eta zein OT-n.
- Mugatu kasu gehienetan OT-ko sistemak kanpoko sareetara ez ikustea.
- Ezarri irizpideak, adibidez:
  - lanpostu batetik OT-ra sarbidea ez da baimendu zuzenean
  - ariketa/maintenimendu lanetarako soilik jump host bat
  - SCADA edo historian zerbitzari batera sarbidea mugatu

### 3. Firewall edo pfSense konfiguratu
- Instalatu edo erabili router/firewall birtuala.
- Sortu arau multzoak eremu bakoitzerako.
- Konfiguratu baliozko politika guztiak, adibidez:
  - IT -> DMZ: baimenduta
  - IT -> OT: ukatuta, salbuespenak soilik
  - DMZ -> OT: baimenduta zerbitzu zehatzetarako
  - OT -> Internet: gehienetan ukatuta

### 4. Zero Trust printzipioa aplikatu
- Ezarri arau zehatzak eta minimoa den baimenak.
- Saihestu "edozeinetik edozeinera" sarbidea.
- Definizio zehatzak erabili:
  - IP-etan oinarritutako arauak
  - portu zehatzetarako baimenak
  - erabiltzaile edo makina bati lotutako sarbidea

### 5. Jump host edo bastioia konfiguratu
- Sortu zerbitzari edo makinazaletasun bat, administrazio-lanetarako bakarrik.
- Mugatu jump host-a OT-rekin komunikatzeko soilik portu eta prozedura zehatzetan.
- Funtsezkoa da administrazio-trafikoa zentralizatzea eta oinarri segurua izatea.

### 6. Proba egin
- Saiatu IT sareko makinatik OT sistemara sarbidea lortzen.
- Emaitza dokumentatu: arau desberdinen arabera baimendu edo ukatu behar dela.
- Probatu administrazio lanetarako jump host baten bidez soilik sarbidea funtzionatzen duela.

### 7. Dokumentatu emaitzak
- Sortu taula bat arau bakoitzerako: norena, zertarako, baimenduta/ukatuta eta zergatik.
- Gehitu sare-diagrama eta ohar penagarriak.

### 8. Ondorioak
- Aztertu zergatik da garrantzitsua segmentazioa industriako inguruneetan.
- Idatzi zein arrisku murrizten diren arau hauekin eta zer eragiketa-aldagai dauden zaurgarritasunak murrizteko.
