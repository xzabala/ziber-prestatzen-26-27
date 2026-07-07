# RA10. IT/OT integrazioa

## Laburpena
RA10k IT (Information Technology) eta OT (Operational Technology) sistemak integratzeko eta segurtatzeko oinarrizko printzipioak lantzen ditu. Dokumentu honek arriskuak identifikatzeko, sareen segmentaziorako, Purdue ereduan oinarritutako geruzen bereizketarako eta SCADA/PLC sistemak babesteko ikuspegi praktikoa eskaintzen du.

## Tresna eta teknologiak sakonki

1. **OpenPLC / ScadaBR**
   - Automatizazioaren irakaskuntzarako software librea erabiltzeko modu eraginkorra.
   - OpenPLCk PLC bat simulatu eta aginduak jaso ditzake.
   - ScadaBR eta HMI sistemek prozesu industrialaren egoera urrunetik ikus dezakete.

2. **Factory I/O**
   - Simulazio industrial 3D indartsua.
   - Modbus TCP bidez OpenPLC-rekin konektatutako muntaiak eraiki daitezke, fisikoki eragina duten egoerak erakusteko.

3. **Kali Linux eta Moki**
   - Auditoriako eta erasoen azterketarako distribuzioak. Moki bereziki erabilgarria da industria-kontrolaren azpiegiturari buruzko tresnekin.

4. **Nmap / Shodan / Metasploit (ICS moduluak)**
   - Shodan "gauzen bilatzailea" da eta PLC ahulak aurkitzeko erabilgarria da.
   - Nmap-ek Modbus edo S7 bezalako script espezifikoak ditu sare lokaleko PLCak aurkitzeko.
   - Metasploit-ek SCADA/ICS protokoloei eragiten dieten moduluak eta exploit-ak ditu.

5. **Conpot (honeypot industriala)**
   - OT sistemak imitatzen dituen honeypot aurreratua, erasotzaileei engainua emateko diseinatua.

## Ariketa praktikoak

- [Ariketa 1: Prozesu industrialaren simulazioa](Ariketa1_Prozesu_industrialaren_simulazioa.md)
- [Ariketa 2: Segmentazioa eta isolamendua](Ariketa2_Segmentazioa_eta_aislamientoa.md)
- [Ariketa 3: PLCaren enumerazioa eta esplotazioa simulatu](Ariketa3_PLC_enumerazioa_eta_explotazioa.md)
- [Ariketa 4: Defentsa-inteligentzia eta Conpot](Ariketa4_Inteligentzia_defentsiboa_Conpot.md)

## Ariketen laburpena

### Ariketa 1: Prozesu industrialaren simulazioa
- IT eta OT artean dauden arkitektura-desberdintasunak ulertzea.
- PLC, SCADA eta HMI sistema batzuen funtzionamendua praktikan ezagutzea.

### Ariketa 2: Segmentazioa eta isolamendua
- IT eta OT sareen arteko mugak ezartzea.
- Malwareak edo erasoek planta industrialera iristea eragozteko politika eta arauak aplikatzea.

### Ariketa 3: PLCaren enumerazioa eta esplotazioa simulatu
- PLC baten aurkikuntza eta azterketa egitea sare lokal batean.
- Segurtasunik eza duten inguruneetan izan daitezkeen ondorio fisikoak ulertzea.

### Ariketa 4: Defentsa-inteligentzia eta Conpot
- OT inguruneetan intrusioak goiz detektatzeko metodoak ezagutzea.
- Honeypot industrial baten erabilpena eta alerten sorrera aztertzea.
