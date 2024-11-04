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
