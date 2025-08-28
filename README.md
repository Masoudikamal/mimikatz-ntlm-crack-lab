# Mimikatz NTLM-crack — lab

## Prosjektpresentasjon
Jeg opprettet en testbruker i et Windows-domene, hentet brukerens NTLM-hash med **Mimikatz**, og bekreftet passordet ved å cracke hashen med **John the Ripper** — alt i et lukket, fiktivt labmiljø.

### Mål
- Opprette lab-bruker (Txxxx) og bekrefte pålogging
- Ekstrahere NTLM-hash lokalt med Mimikatz
- Verifisere passord ved cracking (John)

### Miljø
- Windows Server (AD) + Windows-klient (lab)
- Kali Linux (for John)
- Verktøy: Mimikatz, PowerShell, John the Ripper

### Fremgang (høydenivå) m/ evidens
**1) Brukeropprettelse i AD**  
![AD new user](images/ad-new-user-1.png)
![AD password](images/ad-new-user-2.png)

**2) Innloggingstest**  
![Logon OK](images/login-t50309.png)

**3) Hent Mimikatz og ekstraher påloggingsdata**  
![PowerShell download](images/pwsh-download-mimikatz.png)  
![Zip extract](images/mimikatz-extract.png)  
![Mimikatz #1](images/mimikatz-logonpasswords-1.png)  
![Mimikatz #2 (NTLM)](images/mimikatz-logonpasswords-2.png)

**4) Forbered hashfil og crack i John**  
Format: `bruker:NTLMhash` (én linje).  
![Skriv hash til fil](images/write-hash-to-file.png)  
![John crack](images/john-crack-ntlm.png)

### Læringspoeng
- Lokale minne-dump av påloggede creds er farlige uten EDR/LSA-beskyttelse.  
- Svake/gjenbrukte passord gjør cracking triviell.  
- Forsvar: Credential Guard/LSA Protection, sterke passord, 2FA, begrense RDP, logg/alerting.

> Etikk: Alt gjort i avgrenset lab. Sladd domener/IP/kandidatnr. ved publisering.

## Lisens
MIT
