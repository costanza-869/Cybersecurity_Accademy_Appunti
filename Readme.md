#APPUNTI COMANDI WINDOWS

[Per collegarsi in ssh:
-	Apri il terminale
-	Scrivo ssh username@indirizzo IP  
[Se ssh non gira sulla porta 22, devo scrivere    ssh username@indirizzoIP -p numeroporta]

vedi Tryhackme https://tryhackme.com/r/room/windowscommandline 
Comando `tracert`
--> (traceroute) mostra il percorso dall’indirizzo IP iniziale a quello finale.

`nslookup`
--> comando che mi dà informazioni sui record (A, AAAA, CNAME e MX)

`netstat`
--> comando per vedere tutte le connessioni stabilite tra le macchine, comprende anche i numeri di porta e il PID.  

| “pipe” --> serve per collegare due comandi praticamente. Ad esempio:
`netstat -abon | findstr 3389`
--> comando per cercare cosa gira sulla porta 3389 senza usare il 
				comando Grep.

`tasklist`

--> comando che mi dice tutti i programmi che stanno lavorando all’interno della macchina virtuale
whois nomesito.it --> mi dà una serie di informazioni (data di creazione, data di scadenza…)



#I RECORD
Esistono diversi tipi di record:
-	tipo A --> collega un nome di dominio a un indirizzo IP, indicando dove inviare il traffico web per quel dominio.
Facendo ping o nslookup --> con questi due comandi ottengo il record di tipo A, che corrisponde infatti all’indirizzo IP.
In uno stesso server ci possono essere più siti internet. 

`Nslookup -type=A sitoweb.it`

-	tipo AAAA --> utilizzato per risolvere, cioè creare una corrispondenza tra un nome a dominio ed un indirizzo IPv6.

`Nslookup -type=AAAA sitoweb.it`


-	tipo CNAME --> Canonic Name Record --> associa un dominio alternativo a un dominio canonico; consente di creare un alias per un nome di dominio esistente. Mi permette di creare dei sottodomini. 
Ad esempio: viaggi.conad.it  il dominio principale è conad.it, hanno creato il sottodominio “viaggi” che corrisponde al CNAME.

`Nslookup -type=CNAME sitoweb.it`


-	MX Record  dice principalmente dove sono collocati i server di posta elettronica. Sarebbe “Mail Exchange Record”.

Dig mx nomesito.it
`Nslookup -type=mx nomesito.it`

--> Questi due comandi mi portano allo stesso risultato: vedere quale indirizzo di posta elettronica ha questo sito.
[Quando si invia o si riceve un messaggio di posta elettronica, questo arriva su un server. Infatti si può accedere alla posta elettronica da qualsiasi computer]
Per capire dov’è la posta elettronica di una società, di un’azienda devo guardare il record MX. 


-	TXT Record --> contengono informazioni che aiutano i server e i servizi di rete esterni a gestire le email in uscita dal dominio. Per verificare la proprietà del dominio, garantire la sicurezza delle email ed evitare spam e phishing.


