
# NETBIRD v0.72.2 INSTALATZEA ETA KONFIGURATZEA
(cc-by-nc-sa TKnikak garatutako dokumentuan oinarritu)
Data: 2026ko uztaila
NetBird bertsioa: v0.72.2 (Unekoa)
Helburu sistema eragilea: Ubuntu 26.04

AURKIBIDEA
----------
1. Azpiegitura-eskakizunak
2. Zerbitzariaren hasierako konfigurazioa
3. Domeinuaren konfigurazioa (DNS)
4. Menpekotasunak instalatzea
5. NetBird instalatzea (self-hosted zerbitzaria)
6. Alderantzizko proxy-a konfiguratzea (Traefik)
7. Lehen abiaraztea (onboarding)
8. NetBird bezero bat konektatzea
9. Erabiltzaileak kudeatzea
10. Mantentze-lanak eta eguneraketak
11. Arazo ohikoen konponbidea

## 1. AZPIEGITURA-ESKAKIZUNAK

Hardware gutxienekoa:
  - 1 CPU birtuala (gutxienez), 2 vCPU gomendatua
  - 2 GB RAM (gutxienez), 4 GB gomendatua
  - 20 GB biltegiratzea

Sarea:
  - IP publiko bat, eskuragarri hauetan:
      TCP 80   → Let's Encrypt / HTTP birbideratzea
      TCP 443  → Dashboard, API, HTTPS seinalizazioa
      UDP 3478 → STUN/TURN (WireGuard seinalizazioa)
      UDP 51820 → WireGuard (peer-en arteko datu-trafikoa, hautazkoa)

Softwarea:
  - Docker Engine (>= 24.x)
  - Docker Compose plugin (>= 2.x)
  - curl
  - jq


## 2. Zerbitzariaren hasierako konfigurazioa

- Makina sortu, SSH aktibatuta eta dagokion IPa ezarrita
- SSH bidez konektatu eta ondokoak egin
    - Sistema eguneratu

        ```bash
        apt update && apt upgrade -y
        ```

    - Oinarrizko tresnak instalatu

        ```bash
        apt install -y curl wget git htop ufw
        ```
- Suebakiaren konfigurazioa (UFW)
    - SSH baimendu
        ```bash
        ufw allow 22/tcp
        ```

    - HTTP/HTTPS trafikoa baimendu (Let's Encrypt eta dashboard-erako)
        ```bash
        ufw allow 80/tcp
        ufw allow 443/tcp
        ```

    - NetBird STUN/TURN portua baimendu (seinalizazioa)
        ```bash
        ufw allow 3478/udp
        ```

    - WireGuard baimendu (peer-en arteko zuzeneko konexioa)
        ```bash
        ufw allow 51820/udp
        ```
    - Suebakia gaitu
        ```bash
        ufw enable
        ufw status
        ```
## 3. DOMEINUAREN KONFIGURAZIOA (DNS)


Instalazio-scripta exekutatu aurretik, domeinu bat eduki behar duzu
VPS-aren IP publikora bideratua.

Adibidea: netbird.adibidea.eus

DNS erregistroak sortu behar dituzu domeinu-hornitzailean:

  Mota   | Izena              | Balioa                   | Proxy
  -------|--------------------|--------------------------|---------
  A      | netbird            | <VPS_IP_PUBLIKOA>        | DNS soilik
  CNAME  | *.netbird          | netbird.adibidea.eus     | DNS soilik

OHARRA: Cloudflare erabiltzen baduzu, proxy-a desaktibatu
(laranja hodeia → grisa) NetBird-en erregistroetan. TLS ziurtagiriak
Traefik-ek kudeatzen ditu zuzenean Let's Encrypt bidez.

DNS erregistroak hedatzen itxaron (10 minutu arte har dezake).
Egiaztatu hau exekutatuz:
  dig +short netbird.adibidea.eus
  # VPS-aren IP publikoa itzuli behar du

## 4. MENPEKOTASUNAK INSTALATZEA

### 4.1 Docker Engine instalatzea

- Docker instalatu script ofizialaren bidez

    ```bash
    curl -fsSL https://get.docker.com | sh
    ```

- Instalazioa egiaztatu

    ```bash
    docker --version
    docker compose version
    ```

- (Hautazkoa) Zure erabiltzailea docker taldean gehitu sudo saihestu ahal izateko

    ```bash
    usermod -aG docker $USER
    ```

### 4.2 jq instalatzea

```bash
apt install -y jq
```

- Egiaztatu
    ```bash
    jq --version
    curl --version
    ```

## 5. NETBIRD INSTALATZEA (SELF-HOSTED ZERBITZARIA)

### 5.1 Lan-direktorioa sortzea
```bash
mkdir -p /opt/netbird
cd /opt/netbird
```

### 5.2 Instalazio-scripta deskargatu eta exekutatu
- NetBird v0.72.2 script ofiziala
```bash
curl -fsSL https://github.com/netbirdio/netbird/releases/latest/download/getting-started.sh | bash
```

- Script interaktiboak hau galdetuko dizu:

    - Oinarrizko domeinua (adibidea: netbird.adibidea.eus)
     DNS-an konfiguratu duzun FQDN-a sartu.

    - Alderantzizko proxy-aren hautaketa:
     Which reverse proxy will you use?
        - [0] Traefik (gomendatua - TLS automatikoa, Docker Compose-n sartuta)
        - [1] Traefik existentea (kanpoko Traefik instantziarako etiketak)
        - [2] Nginx (konfigurazio-txantiloia sortzen du)
        - [3] Nginx Proxy Manager
        - [4] Kanpoko Caddy
        - [5] Bestea/Eskuzkoa

         → Sakatu Enter [0] Traefik aukera onartzeko (gomendatua)

    - NetBird Proxy zerbitzua gaitu:
        - Do you want to enable the NetBird Proxy service? [y/N]

         → Erantzun 'y' barne baliabideak Interneten esposatu nahi badituzu
       dashboard-aren bidez. Geroago ere gaitu daiteke.

### 5.3 Script-ak sortutako fitxategiak
Script-ak honako fitxategiak sortzen ditu uneko direktorioan:

  - docker-compose.yml  → Edukiontzi guztien konfigurazioa
  - config.yaml         → Konfigurazio bateratua (management, signal,
                         relay, STUN)
  - dashboard.env       → Dashboard-aren ingurune-aldagaiak
  - proxy.env           → Proxy-aren aldagaiak (soilik gaitu bada)

### 5.4 Zerbitzuak abiaraztea
- Script-ak automatikoki abiarazten ditu. Eskuz kudeatzeko:
    ```bash
    cd /opt/netbird
    ```

- Edukiontzien egoera ikusi
    ```bash
    docker compose ps
    ```

- Erregistroak denbora errealean ikusi
    ```bash
    docker compose logs -f
    ```

- Zerbitzu guztiak gelditu
    ```bash
    docker compose down
    ```

- Zerbitzu guztiak berrabiarazi
    ```bash
    docker compose restart
    ```

## 6. ALDERANTZIZKO PROXY-A KONFIGURATZEA (TRAEFIK)

[0] Traefik aukerarekin, alderantzizko proxy-a docker-compose.yml
fitxategian sartuta dago eta ez du konfigurazio gehigarririk behar.

Traefik-ek automatikoki kudeatzen du:
  - TLS ziurtagiriak Let's Encrypt bidez (automatikoki berritzen ditu)
  - HTTP → HTTPS birbideratzea
  - Dashboard-era, management-era, signal-era eta relay-ra bideratzea

Traefik-ek ziurtagiriak lortu dituela egiaztatu:
```bash
docker compose logs traefik | grep -i "certificate"
```

Ziurtagiria ez bada ematen, egiaztatu:
  1. 80 eta 443 portuak suebakian irekita daudela
  2. Domeinuaren DNS VPS-aren IP-ra zuzen bideratuta dagoela
  3. Let's Encrypt-en muga ez duzula gainditu (5 domeinu/astean)

## 7. LEHEN ABIARAZTEA (ONBOARDING)

### 7.1 Administratzaile-kontua sortzea
1. Ireki nabigatzailea eta joan: https://netbird.adibidea.eus
2. Setup orrira birbideratuko zaitu: https://netbird.adibidea.eus/setup
3. Bete formularioa:
   - Administratzailearen helbide elektronikoa
   - Izena
   - Pasahitz sendoa
4. Egin klik "Create Account" aukeran

OHARRA: /setup orria soilik eskuragarri dago erabiltzailerik ez dagoenean.
Lehen kontua sortuz gero, ohiko login orrira birbideratzen du.

### 7.2 Dashboarda atzitzea egiaztatu
- Joan https://netbird.adibidea.eus helbidera
- Saioa hasi administratzailearen kredentzialak erabiliz
- NetBird panela ikusi beharko zenuke (Peers, Networks, etab.)

### 7.3 Setup Key bat lortzea
Setup Key-ak sare berrian peer berriak (bezeroak) erregistratzeko erabiltzen dira.

1. Dashboard-ean, joan: Setup Keys atalera
2. Setup Key berri bat sortu:
   - Izen deskriptiboa (adib. "produkzio-zerbitzariak")
   - Mota: Reusable (peer ugari erregistratzeko) edo One-off
   - Taldeak: sare-taldeak esleitu konfiguratu badituzu
   - Iraungipena: hautazkoa
3. Sortutako gakoa kopiatu (behin bakarrik erakusten da)

## 8. NETBIRD BEZERO BAT KONEKTATZEA (PEER)

### 8.1 NetBird instalatzea Linux-en (bezeroa)
- Bezero ekipoan:
    ```bash
    curl -fsSL https://pkgs.netbird.io/install.sh | sh
    ```

- Edo instalazio script zuzenarekin:
    ```bash
    curl -fsSL https://github.com/netbirdio/netbird/releases/latest/download/install.sh | sh
    ```

### 8.2 Bezeroa self-hosted zerbitzarira konektatu
------------------------------------------------
- Ordeztu balioak zure instalaziokoenekin:
    ```bash
    netbird up \
    --management-url https://netbird.adibidea.eus \
    --setup-key <KOPIATUTAKO_SETUP_KEY>
    ```


### 8.3 Konexioa egiaztatu
-----------------------
- Peer-aren egoera ikusi
    ```bash
    netbird status
    ```

- Konektatutako peer-ak ikusi
    ```bash
    netbird peers
    ```

- Konektagarritasuna egiaztatu (overlay sarearen IP-a, normalean 100.x.x.x)
    ```bash
    ping 100.x.x.x
    ```

### 8.4 NetBird instalatzea Windows/macOS-en
- Deskargatu instalatzailea: https://github.com/netbirdio/netbird/releases/tag/v0.72.2
- Exekutatu instalatzailea eta jarraitu argibideak
- Konfigurazioan, sartu zerbitzariaren URLa:
    https://netbird.adibidea.eus
- Erabili Setup Key peer-a erregistratzeko


## 9. ERABILTZAILEAK KUDEATZEA

NetBird-ek tokiko erabiltzaile-kudeaketa barne hartzen du, Dex
zerbitzari integratuaren bidez (kanpoko nortasun-hornitzailerik gabe).

### 9.1 Erabiltzaile berriak sortzea
1. Joan dashboard-era → Settings → Users
2. Egin klik "Add User" aukeran
3. Sartu helbide elektronikoa, izena eta pasahitza
4. Esleitu rola: Admin edo User

### 9.2 Taldeen eta sarbide-politiken kudeaketa
1. Joan → Access Control → Groups
2. Sortu taldeak peer-ak antolatzeko (adib. "zerbitzariak", "langileak")
3. Joan → Access Control → Policies
4. Sortu politikak zein peer-ek elkarrekin komunikatu daitezkeen zehazteko

### 9.3 Kanpoko nortasun-hornitzaileak (SSO, hautazkoa)
NetBird-ek SSO onartzen du honako hornitzaileekin:
  - Google Workspace
  - Microsoft Entra ID (Azure AD)
  - Okta
  - GitHub
  - OIDC bateragarria den edozein hornitzaile

Konfigurazioa: Settings → Identity Providers

## 10. MANTENTZE-LANAK ETA EGUNERAKETAK

### 10.1 NetBird azken bertsiorako eguneratzea

- Docker irudi berriak deskargatu
    ```bash
    cd /opt/netbird
    docker compose pull
    ```

- Edukiontziak irudi berriekin berrabiarazi
    ```bash
    docker compose up -d
    ```
- Dena ondo dagoela egiaztatu
    ```bash
    docker compose ps
    ```

### 10.2 Datuen babeskopia
- Datu garrantzitsuen kokapenak:
    - /opt/netbird/config.yaml         → Zerbitzariaren konfigurazioa
    - /opt/netbird/docker-compose.yml  → Zerbitzuen definizioa
    - /opt/netbird/dashboard.env       → Dashboard-aren aldagaiak

- Docker bolumenak (datu-basea, ziurtagiriak):
    ```bash
    docker volume ls | grep netbird
    ```

- Babeskopia osoa:
    ```bash
  tar -czf netbird-babeskopia-$(date +%Y%m%d).tar.gz \
    /opt/netbird/ \
    $(docker volume inspect netbird_data --format '{{.Mountpoint}}')
    ```

### 10.3 Monitorizazioa
- Zerbitzu guztien erregistroak ikusi
    ```bash
    docker compose logs -f
    ```

- Zerbitzu zehatz baten erregistroak ikusi
    ```bash
    docker compose logs -f management
    docker compose logs -f signal
    docker compose logs -f relay
    docker compose logs -f dashboard
    ```

- Baliabideen erabilera ikusi
    ```bash
    docker stats
    ```

## 11. ARAZO OHIKOEN KONPONBIDEA

- Arazoa: Ezin dut /setup orrira sartu
    - → /setup orria soilik dago eskuragarri erabiltzailerik ez dagoenean.
    Erabiltzaile bat sortu baduzu, joan zuzenean loginera:
    https://netbird.adibidea.eus

- Arazoa: TLS ziurtagiria ez da ematen
    - → Egiaztatu 80 eta 443 portuak Internetik eskuragarri daudela
    - → Domeinuaren DNS VPS-aren IP-ra zuzen bideratuta dagoela berretsi
    - → Traefik-en erregistroak berrikusi: docker compose logs traefik

- Arazoa: Peer-ak ez dira konektatzen
    - → Egiaztatu UDP 3478 portua suebakian irekita dagoela
    - → Bezeroaren management URL zuzena dela egiaztatu
    - → Erabilitako Setup Key iraungitu ez dela egiaztatu
    - → Berrikusi: docker compose logs management

- Arazoa: Bezeroak "disconnected" erakusten du
    - → Exekutatu: netbird down && netbird up --management-url https://...
    - → Bezeroaren sarekiko konektagarritasuna egiaztatu

- Arazoa: Admin pasahitza ahaztu dut
    → Sartu dashboard-era beste admin erabiltzaile batekin
    → Edo sortu erabiltzaile berri bat API bidez PAT (Personal Access Token) batekin

----------------------------------------------------------------------
Laguntza gehiagorako:
  - Dokumentazio ofiziala: https://docs.netbird.io
  - Komunitate Slack-a: https://netbird.io/slack
  - GitHub Issues: https://github.com/netbirdio/netbird/issues
----------------------------------------------------------------------