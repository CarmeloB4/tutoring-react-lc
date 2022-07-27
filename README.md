<img src="https://user-images.githubusercontent.com/66789080/179777872-875ab38b-816d-4a2d-ae9a-aa35010973f3.png" width="100px" />

# 🛒 React Shop Project
Lo scopo di questo progetto è quello di ricreare quanto visto nella live coding, questa repository nasce come guida per chi, passo dopo passo, vuole replicare quanto fatto insieme. <br/>
## How to work
Potete forkare questa repository e lavorare tranquillamente alla vostra soluzione, il branch di partenza sarà il <code>main</code>. Oltre questo troverete dei branch che contengono le varie soluzioni.
<br>
Affronteremo questo progetto step by step, in modo tale che chi segue questa guida può autonomamente andare avanti, anche magari sbirciando dalle soluzioni. Cercherò comunque di inserire più commenti e riferimenti esterni (link a documentazione, ect..) possibili.

## Step 
### Creazione del progetto
Partiamo dallo script che crea il nostro boilerplate del progetto React, basta lanciare quindi <code>npx create-react-app <nome progetto></code><br>
Nel nostro caso, il progetto è stato già creato e si trova nella cartella react-shop (dovrete poi lanciare <code>npm i</code> per installare i node_modules)
### Aggiunta di Bootstrap o Tailwind
Per aggiungere bootstrap al nostro progetto basterà seguire questa documentazione: https://create-react-app.dev/docs/adding-bootstrap/ <br>
A mio avviso, risulta molto più semplice ed immediato inizialmente lavorare con Bootstrap.
### Differenza tra Class componente e Functional Component
Dalla versione 16.8 di React, abbiamo avuto l'introduzione degli hooks e altre interessanti feature senza l'utilizzo delle classi. Da adesso in poi, i nostri componenti saranno dei functional component, tecnicamente delle funzioni pure di Javascript che ritornano un elemento React (JSX). Nelle classi invece dovevamo prima di tutto estendere la nostra classe a React, e la nosta classe ritornava una funzione <code>render</code>. <br>
Una grossa differenza è anche nella gestione dello stato e del lifecycle (ciclo di vita) del nostro componente. Adesso con i FC non dobbiamo più preoccuparci di questo, avremo infatti degli hooks per andare a gestire l'inizializzazione del componente. Nella classe invece, si trovavano dei metodi specifici che andavano a gestire tutti i cicli di vita della classe (mount, rendering, unmount).
### Utilizziamo gli hooks
Esistono diversi hooks in React, tanti di questi in realtà per varie esigenze non verrano mai utilizzati, altri invece sono fondamentali. <br>
Quelli che andremo ad utilizzare in questo progetto sono essenzialmente i principalo, parliamo di:
- useState
- useEffect
### A cosa serve avere uno stato? (useState)
Uno stato ci serve per avere una proprietà, all'interno del nostro componente, che può essere inizialiazzata anche con un valore iniziale (oppure no), e possiamo anche aggiornare il valore di quella proprietà. <br>
Doc: https://it.reactjs.org/docs/hooks-state.html
### Come funziona useEffect?
Se avete già visto le classi, in pratica useEffect non è nient'altro che componentDidMount, componentDidUpdate, e componentWillUnmount messi insieme. <br>
Questo hook viene chiamato quando il componente viene inizializzato (mount), e può restare in ascolto di alcune 'dipendenze' (proprietà, variabili, funzioni) in modo tale da essere ritriggherato.
### Come strutturare il progetto
Andiamo a vedere l'architettura del nostro progetto: <br>
![structure](https://user-images.githubusercontent.com/66789080/180755750-9af144dd-892b-4429-8425-48f46ee3d480.png)
<br>
Come vedete ho creato due cartelle:
- Pages (lì andremo a mettere le pagine della nostra applicazione, es. Home, Contatti, Dashboard, Lavora con noi)
- Components (qui invece mettiamo tutti i vari componenti che possono andare ad essere inseriti (quindi comporre) la pagina, solitamente creaimo dei componenti cosidetti shared, cioè condividi in tutta l'applicazione)
<br>
Dietro questa divisione abbiamo un ragionamento preciso, l'obiettivo è quello di realizzare la nostra app secondo dumb component e smart component
Articolo: https://javascript.plainenglish.io/react-all-about-components-35650a02ff50 <br>
In poche parole, avremo componenti (quindi quelli sotto la cartella pages) che avranno al loro interno la logica, ed altri componenti (quelli sotto components) che prenderanno solo dati in input (props) e si occuperanno solamente della UI <br>

### Creazione dei componenti shared
Come dicevamo i componenti shared avranno la sola responsabilità di 'mostrare' i dati, non andremo a mettere logica al loro interno. Un esempio sono: navbar e footer.
### Creazione della pagina
La nostra pagina 'Home' conterrà tutta la logica della nostra piccola applicazione, in modo tale da rendere più semplice il passaggio di proprietà tra i vari componenti. <br>
Un aspetto fondamentale infatti è la comunicazione tra componente padre e figlio, un problema che pongo sempre è, dobbiamo realizzare la nostra app in modo tale che il padre passi un dato ad un figlio, e se il figlio compie un azione al suo interno (CTA - call to action, può essere un bottone acquista), la logica di 'acquisto' deve essere contenuta nel padre. <br>
Più in avanti vedrete Redux che semplificherà un po' le cose.
### Come utilizzare useState e useEffect
Nel nostro caso abbiamo bisogno di due stati iniziali. <br>
![state](https://user-images.githubusercontent.com/66789080/180780495-d085a615-1c57-46d2-970a-975e8e8359b0.png) <br>
Nel primo stato andiamo ad indicare tutti i prodotti, nel secondo stato invece, andiamo ad indicare i prodotti aggiunti al carrello.
Per iniziallizare il nostro stato, utilizzeremo l'useEffect in modo tale che al rendering della pagina andremo a 'riempire' il nostro stato (meglio definire tecnicamente, settare il nostro stato). <br>
![effect](https://user-images.githubusercontent.com/66789080/180781563-aead4413-4c57-4e9c-9540-9e7270071031.png) <br>
Al momento immaginiamo data come array di oggetti, nel bonus step, il nostro data sarà in realtà il risultato di una chiamata API.
### Comunicazione tra componenti
Come dicevamo, abbiamo diviso la nostra applicazione in smart components e dummy components, quindi dobbiamo passare dei dati tra componenti. Questa operazione su React possiamo farla attraverso le props. <br>
Il concetto di props consiste nel passaggio di dati tra padre e figlio. In questo modo possiamo organizzare la logica in componenti principali e passare i dati a componenti figli. <br>
Doc: https://it.reactjs.org/docs/components-and-props.html

## Bonus step
### Aggiungiamo la navigazione
Immaginate adesso di avere un paio di pagine in più, oltre alla nostra Home, avremo alvre due pagine <code>Contacts</code> e <code>About us</code>. <br>
Per raggiungere queste pagine intanto, dovremmo inserire delle voci nella nostra Navbar, che quindi avrà tre link: Home, Contacts, About us. Per gestire la navigazione con React, abbiamo bisogno di una libreria: https://github.com/remix-run/react-router#readme <br>
Grazie alla libreria <code>react-router</code> possiamo facilmente aggiungere la navigazione tra pagine alla nostra applicazione.
Qui un semplice esempio: https://v5.reactrouter.com/web/example/basic
### Chiamate di rete
Per rendere la nostra applicazione completa, possiamo aggiungere finalmente la chiamata di rete, per far questo, dovete almeno avere conoscenza di come funzionano le chiamate asincrone con Javascript. <br>
Inizialmente, possiamo gestire la nostra chiamata tramite il classico <code>fetch</code> https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch <br>
L'API dalla quale vogliamo attingere è la seguente: https://db.ygoprodeck.com/api/v7/randomcard.php <br>
Modificate quindi la nostra applicazione in base alla risposta della API (prima avevamo un array di oggetti, invece adesso?) <br>
<br>
*dopo aver lavorato con il fetch, provate questa libreria: https://swr.vercel.app/docs/getting-started
### Aggiungiamo redux
*questa sarà la parte più complessa della nostra applicazione
