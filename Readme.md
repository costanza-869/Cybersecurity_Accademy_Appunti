14/10/2024 1a lezione

APPUNTI COMANDI WINDOWS

[Per collegarsi in ssh:
-	Apri il terminale
-	Scrivo ssh username@indirizzo IP  
[Se ssh non gira sulla porta 22, devo scrivere    ssh username@indirizzoIP -p numeroporta]

vedi Tryhackme https://tryhackme.com/r/room/windowscommandline 
Comando tracert --> (traceroute) mostra il percorso dall’indirizzo IP iniziale a quello finale.

Nslookup --> comando che mi dà informazioni sui record (A, AAAA, CNAME e MX)

Netstat --> comando per vedere tutte le connessioni stabilite tra le macchine, comprende anche i numeri di porta e il PID.  

| “pipe” --> serve per collegare due comandi praticamente. Ad esempio:
netstat -abon | findstr 3389  comando per cercare cosa gira sulla porta 3389 senza usare il 
				comando Grep.

tasklist --> comando che mi dice tutti i programmi che stanno lavorando all’interno della macchina virtuale
'''whois nomesito.it''' --> mi dà una serie di informazioni (data di creazione, data di scadenza…)
