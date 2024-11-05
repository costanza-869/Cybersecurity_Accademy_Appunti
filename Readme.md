**#APPUNTI COMANDI WINDOWS#**

[Per collegarsi in ssh:
-	Apri il terminale
-	Scrivo ssh username@indirizzo IP  
[Se ssh non gira sulla porta 22, devo scrivere    ssh username@indirizzoIP -p numeroporta]

vedi Tryhackme https://tryhackme.com/r/room/windowscommandline 
Comando --> (traceroute) mostra il percorso dall’indirizzo IP iniziale a quello finale.


```
tracert
```


```
nslookup`
```

--> comando che mi dà informazioni sui record (A, AAAA, CNAME e MX)

```
netstat
```

--> comando per vedere tutte le connessioni stabilite tra le macchine, comprende anche i numeri di porta e il PID.  

| “pipe” --> serve per collegare due comandi praticamente. Ad esempio:

```
netstat -abon | findstr 3389
```

--> comando per cercare cosa gira sulla porta 3389 senza usare il 
				comando Grep.

```
tasklist
```

--> comando che mi dice tutti i programmi che stanno lavorando all’interno della macchina virtuale


```
whois nomesito.it 
```


--> mi dà una serie di informazioni (data di creazione, data di scadenza…)



**#I RECORD#**
Esistono diversi tipi di record:
-	tipo A --> collega un nome di dominio a un indirizzo IP, indicando dove inviare il traffico web per quel dominio.
Facendo ping o nslookup --> con questi due comandi ottengo il record di tipo A, che corrisponde infatti all’indirizzo IP.
In uno stesso server ci possono essere più siti internet.


```
Nslookup -type=A sitoweb.it
```

-	tipo AAAA --> utilizzato per risolvere, cioè creare una corrispondenza tra un nome a dominio ed un indirizzo IPv6.

```
Nslookup -type=AAAA sitoweb.it
```


-	tipo CNAME --> Canonic Name Record --> associa un dominio alternativo a un dominio canonico; consente di creare un alias per un nome di dominio esistente. Mi permette di creare dei sottodomini. 
Ad esempio: viaggi.conad.it  il dominio principale è conad.it, hanno creato il sottodominio “viaggi” che corrisponde al CNAME.

```
Nslookup -type=CNAME sitoweb.it
```


-	MX Record  dice principalmente dove sono collocati i server di posta elettronica. Sarebbe “Mail Exchange Record”.

```
Dig mx nomesito.it
```

```
Nslookup -type=mx nomesito.it
```

--> Questi due comandi mi portano allo stesso risultato: vedere quale indirizzo di posta elettronica ha questo sito.
[Quando si invia o si riceve un messaggio di posta elettronica, questo arriva su un server. Infatti si può accedere alla posta elettronica da qualsiasi computer]
Per capire dov’è la posta elettronica di una società, di un’azienda devo guardare il record MX. 

-	TXT Record --> contengono informazioni che aiutano i server e i servizi di rete esterni a gestire le email in uscita dal dominio. Per verificare la proprietà del dominio, garantire la sicurezza delle email ed evitare spam e phishing.

_________________________________________________________________________________________________________________________________________________________________
**Passive Reconnaissance**
Corrisponde alla fase iniziale dell’ethical hacking in cui si raccolgono informazioni su un obiettivo senza interagire direttamente con i suoi sistemi. L'obiettivo è ottenere dati come nomi di dominio, indirizzi IP, email, e informazioni pubbliche, usando solo fonti accessibili (ad esempio, motori di ricerca, social media, WHOIS, registri pubblici). A differenza della ricognizione attiva, non coinvolge alcun contatto con il sistema bersaglio, riducendo così il rischio di essere rilevati.

**CONFRONTO COMANDI RIC. PASSIVA**
1. nslookup

```
nslookup
```
   
Scopo: Effettua ricerche DNS per ottenere l’indirizzo IP di un dominio o il nome di dominio associato a un indirizzo IP (reverse lookup).
Utilizzo:
o	nslookup esempio.com per ottenere l’IP del dominio.
o	nslookup 8.8.8.8 per un reverse lookup (partendo dall’IP risale al nome del dominio).
--> Dando questo 8.8.8.8 io gli sto dicendo “utilizza il DNS 8.8.8.8 e non quello del mio provider”

**Pro**: Semplice e facile da usare, disponibile in quasi tutti i sistemi operativi.
**Contro:** Mostra informazioni limitate e meno dettagliate rispetto a dig.


2. dig
   
```
dig
```
   
Scopo: Esegue ricerche DNS dettagliate per ottenere informazioni complete su un dominio o IP, come i record A, MX, NS, TXT e altro.

Utilizzo:
o	dig esempio.com per un lookup DNS.
o	dig mx esempio.com per ottenere i record MX.
o	dig -x 8.8.8.8 per il reverse lookup.
**Pro**: Output dettagliato e altamente configurabile, con informazioni dettagliate su vari record DNS.
**Contro**: Output più complesso da leggere per chi non è abituato.


4. whois

```
whois
```

Scopo: Ottiene le informazioni di registrazione di un dominio o di un indirizzo IP, inclusi dettagli sull’intestatario, date di creazione e scadenza, registrante, contatti amministrativi e tecnici.

Utilizzo:
o	whois esempio.com per informazioni di registrazione del dominio.
o	whois 8.8.8.8 per i dettagli sull’IP (a chi appartiene).
**Pro**: Fornisce dettagli importanti su proprietà, date di scadenza e registrazione, utili per capire chi possiede il dominio/IP.
**Contro**: Non fornisce informazioni sui record DNS (non è un comando per il lookup DNS).

![image](https://github.com/user-attachments/assets/ad0344b5-e3a4-46e8-8b23-508c7a7c251a)


**Active Reconnaissance**
La ricognizione attiva richiede di stabilire un contatto diretto con il tuo obiettivo. Questo contatto può avvenire tramite una telefonata o una visita alla sede dell'azienda sotto un certo pretesto per raccogliere informazioni, spesso come parte di tecniche di social engineering. In alternativa, può essere una connessione diretta al sistema target, ad esempio visitando il sito web o controllando se la porta SSH del firewall è aperta. È simile all’ispezione ravvicinata di finestre e serrature. È quindi fondamentale ricordare di non intraprendere attività di ricognizione attiva senza prima ottenere un'autorizzazione legale scritta dal cliente.

Il browser web è uno strumento comodo e disponibile su tutti i sistemi, utile per raccogliere informazioni su un obiettivo.

Il browser si connette per impostazione predefinita:
Alla porta TCP 80 per siti web su HTTP
Alla porta TCP 443 per siti web su HTTPS
Queste porte non vengono mostrate nella barra degli indirizzi. Tuttavia, si possono usare porte personalizzate per accedere a specifici servizi, come in https://127.0.0.1:8834/, che apre la connessione all’indirizzo 127.0.0.1 sulla porta 8834 tramite HTTPS.


Durante la navigazione, puoi premere Ctrl+Shift+I su PC o ⌥ + ⌘ + I su Mac per aprire gli Strumenti per sviluppatori su Firefox o Chrome. Questi strumenti permettono di ispezionare elementi come file JavaScript, cookie salvati e la struttura delle cartelle del sito.

**Estensioni utili per il penetration testing**
Esistono anche molte estensioni per Firefox e Chrome che supportano il penetration testing, tra cui:

FoxyProxy: Permette di cambiare velocemente server proxy, utile se si utilizzano strumenti come Burp Suite.
User-Agent Switcher and Manager: Simula l’accesso da dispositivi diversi, ad esempio visualizzando il sito come se si usasse un iPhone.
Wappalyzer: Identifica le tecnologie utilizzate sul sito, raccogliendo informazioni mentre si naviga come un normale utente.
Questi strumenti rendono il browser versatile per raccogliere dati preliminari su un target.

**SCHEMA RIASSUNTIVO FASI DI HACKING**
file:///C:/Users/costa/Downloads/Drawing-204.sketchpad.pdf 

