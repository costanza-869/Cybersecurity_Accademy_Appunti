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

___________________________________________________________________________________________________________________________________________________________________

**NMAP**
vedi room Tryhackme https://tryhackme.com/r/room/furthernmap 

Nell'ambito dell'hacking, la conoscenza è potere: più informazioni si hanno su un sistema o rete target, più opzioni si avranno a disposizione. Per questo motivo, è essenziale eseguire una corretta enumerazione prima di tentare qualsiasi attacco.
Quando si riceve un IP (o una serie di IP) per un audit di sicurezza, il primo passo è ottenere una "mappa" dei servizi attivi sui target. Questo processo inizia con la **scansione delle porte**. Ogni servizio su un computer utilizza una porta per comunicare; ad esempio, un server web potrebbe usare la porta 80 per HTTP e la 443 per HTTPS. Avere questa "mappa" permette di sapere quali servizi sono disponibili e su quali porte, passo necessario per capire come attaccare o testare il sistema.
Ogni computer ha 65535 porte disponibili, molte delle quali sono standard per servizi specifici (ad es., HTTP su porta 80 e HTTPS su 443). Tuttavia, nelle simulazioni di hacking, le porte standard possono essere cambiate, rendendo fondamentale una corretta enumerazione.
Senza sapere quali porte sono aperte, non è possibile attaccare con successo il target. Ecco perché si inizia sempre con una scansione delle porte, generalmente eseguita con uno strumento chiamato nmap. Nmap verifica ogni porta del target per determinarne lo stato (aperta, chiusa, filtrata). Una volta identificate le porte aperte, è possibile verificare i servizi in esecuzione su ciascuna porta.
Perché nmap? È considerato uno standard nel settore per la sua funzionalità avanzata e la capacità di rilevare vulnerabilità, grazie al suo motore di scripting.

Nmap può essere combinato con moltissimi switches per effettuare diversi tipi di scansione; tra i più importanti:

```
nmap -O <target-ip>
```

--> comando per capire quale sistema operativo usa la macchina target


```
nmap -vv <target-ip>
```

--> comando per aumentare la verbosity, per avere più info

```
nmap -oN <filename> <target-ip>
```

--> comando che mi permette di salvare i risultati di nmap in un file formato "normale"

**SCANSIONI STEALTH**
I SYN scan (**opzione -sS**) sono una tipologia di scansione utilizzata per esaminare l'intervallo di porte TCP di un target. A differenza delle scansioni TCP tradizionali, i SYN scan inviano un pacchetto SYN al target e, al ricevimento di un SYN/ACK, rispondono con un pacchetto RST per interrompere la connessione. Questo comportamento impedisce al server di completare la connessione e fare nuovi tentativi di connessione.

Vantaggi dei SYN scan:
- Evasione dei sistemi di rilevamento intrusioni (IDS): Poiché non completano il processo di handshake, possono aggirare gli IDS più vecchi che si basano sulla rilevazione di una connessione completa.
- Stealth: Non vengono generalmente registrati dalle applicazioni in ascolto sulle porte, in quanto la connessione viene registrata solo dopo che è completamente stabilita.
- Velocità: Rispetto alle scansioni TCP tradizionali, i SYN scan sono molto più veloci perché non richiedono di completare il processo di handshake per ogni porta.

Svantaggi dei SYN scan:
- Permessi elevati: Richiedono permessi sudo in Linux per poter inviare pacchetti raw, operazione che solo l'utente root può eseguire.
- Instabilità dei servizi: I SYN scan possono far cadere i servizi instabili, il che può essere problematico in ambienti di produzione.


**CONNESSIONI UDP**
A differenza di TCP, le connessioni UDP sono senza stato. Questo significa che, invece di iniziare una connessione con un processo di handshake (scambio di pacchetti), UDP invia pacchetti a una porta di destinazione sperando che arrivino a destinazione. Questo lo rende ideale per applicazioni che richiedono velocità piuttosto che qualità, come la condivisione di video. Tuttavia, l'assenza di conferma rende la scansione UDP molto più difficile e lenta rispetto a TCP. Il comando Nmap per eseguire una scansione UDP è -sU.

```
nmap -sU <target-ip>
```

Comportamento della scansione UDP:
Porta aperta: Se un pacchetto viene inviato a una porta UDP aperta, non c'è risposta. Nmap la considera open|filtered (aperta o filtrata), poiché non può determinare se la porta sia effettivamente aperta o se sia bloccata da un firewall. Se riceve una risposta UDP (rara), la porta viene segnata come aperta.

Porta chiusa: Se un pacchetto viene inviato a una porta UDP chiusa, il target risponde con un pacchetto ICMP che indica che la porta non è raggiungibile. In questo caso, Nmap la segna come chiusa.

Vantaggi e svantaggi delle scansioni UDP:
Lentezza: Le scansioni UDP sono significativamente più lente rispetto a quelle TCP, richiedendo circa 20 minuti per scansionare i primi 1000 porti con una buona connessione. Per questo motivo, è buona pratica usare l'opzione --top-ports <numero> per scansionare solo le porte più comuni. Ad esempio, nmap -sU --top-ports 20 <target> scansionerà le prime 20 porte UDP più comuni.

Richieste vuote: Nmap invia generalmente pacchetti UDP vuoti, ma per le porte occupate da servizi conosciuti, invia un payload specifico per il protocollo, che ha maggiori probabilità di generare una risposta utile.


**SCANSIONI NULL / FIN / XMAS**
Le scansioni NULL, FIN e Xmas sono tecniche avanzate di scansione delle porte usate in Nmap per **cercare di eludere i sistemi di rilevamento**, come i firewall o i sistemi di intrusion detection (IDS). Queste scansioni sono chiamate "scansioni furtive" perché non stabiliscono una connessione TCP completa, rendendo più difficile la rilevazione.

**Scansione NULL (-sN)**: Non invia alcun flag TCP (nessun SYN, ACK, FIN, ecc.), quindi non può essere facilmente identificata. Le porte aperte non rispondono, mentre le porte chiuse possono rispondere con un pacchetto RST.

**Scansione FIN (-sF)**: Invia un pacchetto TCP con il solo flag FIN, che segnala la fine di una connessione. Le porte chiuse rispondono con un pacchetto RST, mentre quelle aperte generalmente non rispondono affatto.

**Scansione Xmas (-sX)**: Invia un pacchetto con i flag FIN, URG e PSH attivi, creando un pacchetto "illuminato" (da cui il nome Xmas). Come nella scansione FIN, le porte chiuse rispondono con RST, mentre le porte aperte non rispondono.

Queste scansioni sono utili per:
1. Evitare rilevamenti: Possono aggirare alcuni firewall e IDS che si aspettano una connessione TCP completa (SYN, ACK, ecc.).
2. Testare la sicurezza: Sono usate per verificare se un sistema è vulnerabile a queste tecniche o se un firewall o IDS può rilevarle.

**ICMP NETWORK SCANNING**
Per eseguire una ping sweep, si utilizza l'opzione -sn insieme agli intervalli di indirizzi IP, che possono essere specificati con un trattino (-) o con la notazione CIDR. Ad esempio, possiamo scansionare la rete 192.168.0.x con:

```
nmap -sn 192.168.0.1-254
```

oppure

```
nmap -sn 192.168.0.0/24
```

Il flag -sn dice a Nmap di non scansionare alcuna porta, costringendolo a fare affidamento principalmente sui pacchetti di echo ICMP (o richieste ARP su una rete locale, se eseguito con i privilegi di root) per identificare gli host. Inoltre, il flag -sn fa sì che Nmap invii anche un pacchetto TCP SYN alla porta 443 e un pacchetto TCP ACK (o SYN se non eseguito come root) alla porta 80 del target.
