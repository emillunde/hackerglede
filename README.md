# Hackerworkshop Bekk Fagdag 21.10.2022

I denne workshopen skal du bryte deg inn på en ruter, kartlegge nettverket, finne sårbarheter i en webserver og skaffe deg tilgang til serveren og dens database.

## Engasjementsregler

- Det er bare tillatt å angripe wifi-nettverket kalt HackMe og enheter tilknyttet ruterens lokale nettverk på `192.168.38.0/24`.

- Tjenestenektangrep mot ruteren eller andre enheter på nettverket er ikke tillatt da det vil ødelegge for andre.

- Siden alle er koblet på samme nettverk er det lurt å unngå permanente endringer av filer, rettigheter og lignende dersom du skaffer deg tilgang til en server.

## Oppgaver

### 1. Bryt deg inn på wifi-nettverket
Utnytt svakhetene i WPS vha. [OneShot](https://github.com/drygdryg/OneShot) til å skaffe deg passordet til nettverket. Repoet er allerede klonet på maskinen og ligger på rot-nivå. 

<details>
<summary>Hint 1</summary>
Naviger til OneShot-repoet i en terminal og kjør oneshot.py med riktig options.
</details>

<details>
<summary>Hint 2</summary>

Dere må spesifisere riktig trådløst grensesnitt ved å bruke `-i` flagget. Trådløst grensesnitt kan du finne med kommandoen `iwconfig`.
  
</details>

<details>
<summary>Hint 3</summary>
  
Om det tar lang tid, kan det hende dere har glemt å spesifisere hvilket angrep OneShot skal kjøre, ved å kjøre `--pixie-dust`.
</details>

<details><summary>Løsningsforslag</summary>
Kjør kommandoen under, og velg nettverket HackMe.
  
```
sudo python oneshot.py -i wlan0 --pixie-dust
```

</details>

</br>

### 2. Kartlegging
Nå som dere er koblet til nettverket, skal dere finne ut hvilke enheter og hvilke åpne porter som er tilgjengelige. 
Noter eventuelle interessante funn.

<details><summary>Hint 1</summary>

Her kan dere bruke verktøyet `nmap` til å scanne nettverket. Bruk `man nmap` for å se hvilke options dere kan gi til nmap.

</details>

<details><summary>Hint 2</summary>

Enheter som ligger i IP-rangen `192.168.38.100 - 192.168.38.255` er dere selv og andre deltakere i workshopen.

</details>

<details><summary>Løsningsforslag</summary>

Kjør nmap med `-A`flagget for å vise mer informasjon om her host.
  
```sudo nmap -A 192.168.38.0-100```
  
</details>


</br>

### 3. Grav dypere!
Velg dere ut det funnet fra forrige oppgave dere tenker er mest interessant å se videre på. Dere skal nå forsøke å lære litt mer om denne enheten, i jakten på en angrepsvinkel.

a) Finn ut hvilke teknologier som er i bruk på serveren

<details><summary>Hint 1</summary>
Også her er nmap et fint verktøy. Hvilke porter er åpne? Svarer serveren på http/https-trafikk? 
</details>

<details><summary>Hint 2</summary>
Ved å se at port 8080 er åpen, kan vi anta at serveren svarer på https-trafikk. Om dere åpner IP-adressen i en browser får dere nok et hint! 

Om dere ønsker, kan dere også bruke wappalyzer-utvidelsen i nettleseren for å undersøke nærmere. 
</details>
 
b) Se etter skjulte ressurser på serveren ved hjelp av verktøyet `gobuster`. Bruk gjerne en kort ordliste, f. eks. [denne]() for å unngå å overbelaste serveren. 

<details><summary>Hint 1</summary>
Last ned ordlisten og kjør kommandoen under. Ser dere noen interessante funn?

```gobuster dir -u http://192.168.38.72:1337 -w common.txt```
</details>

<details><summary>Løsningsforslag</summary>

Her finnes det flere måter man kan konkludere med at webserveren kjører en wordpress-instans. Man kan feks åpne http://192.168.38.72 i en browser, og se at "Powered by wordpress" pryder footeren på siden. 
  
Ved hjelp av gobuster kan vi også finne frem til siden (TODO TODO TODO TODO TODO TODO)

</br>

### Kjente sårbarheter?

Når man vet hvilken teknologi som brukes er ofte neste steg å finne ut nøyaktig hvilke versjoner som brukes. Deretter kan man undersøke om det er kjente sårbarheter tilknyttet disse versjonene.

<details><summary>Hint</summary>

Kali har et verktøy kalt wpscan som kan gi deg mye informasjon om en Wordpress-server.

</details>

### Bryt deg inn på serveren

### Finn et flagg på serveren

### Skaff deg tilgang til databasen

### Finn et flagg i databasen
