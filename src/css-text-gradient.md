## Applicare un gradiente di colore su un testo

Caro diario,

mi capita spesso, navigando tra i meandri del web, di imbattermi in qualche sito decisamente stravagante e pieno di gadgets innovativi che catturano la mia attenzione per la loro efficacia comunicativa.

Un paio di giorni fa è successo di nuovo.

Pensavo di essermi sbagliato, di aver capito male, non credevo ai miei occhi e soprattuto non capivo perchè un gigante come Google potesse aver fatto un errore cosi grossolano.

Incuriosito da un collegamento che trovai nella homepage del motore di ricerca raggiunsi il nuovo sito di <a href="https://stadia.dev" target="_blank">stadia</a>, l'ultimo prodotto di Google per il gaming. Non ero sicuro di aver ben capito cosa stessi vedendo..

<div class="py-4 px-6">
    <span class="inline-block font-semibold text-3xl" style="background-clip: text; background-image: linear-gradient(107deg,#ff4c1d,#9b0063);color: #9b0063; -webkit-background-clip: text; -webkit-text-fill-color: transparent;">STADIA</span>
</div>

..tutto il sito, pieno di titoli e testo con un gradiente di colore applicato sopra.

Per quel che mi ricordo questo tipo di effetto si poteva ottenere solamente con l'utilizzo di illustrazioni grafiche. Dovevo capire la magia che c'era dietro a tutto questo.

Ecco cosa ho scoperto:

```CSS
.text-gradient {
    background-clip: text;
    background-image: linear-gradient();
    color: ;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}

```

---

## TL;DR

### Toc

* [La tecnica](#tecnica)
* [Supporto](#supporto)
* [Conclusione](#conclusione)
* [Riferimenti](#riferimenti)

<h3 id="tecnica">La tecnica</h3>

La tecnica sfrutta la direttiva CSS `-webkit-background-clip: text` [^1].

Questa direttiva mi permette di creare una sorta di *maschera di ritaglio* (con il testo stesso) da applicare allo sfondo del contenitore del testo.

In abbinamento alla direttiva `-webkit-background-clip: text` è necessario utilizzare anche la regola `-webkit-text-fill-color: transparent` [^2] in modo che il testo risulti trasparente e mi permetta di vedere il gradiente di colore applicato allo sfondo.

Da notare che questa regola ha la precedenza sulla direttiva `color` che viene utilizzata solamente come regola di ripiego nel caso la direttiva non fosse `-webkit-background-clip: text` supportata.

Ci sono alcuni accorgimenti da tenere in considerazione per questa tecnica.

* `background-clip` e `-webkit-background-clip` permettono di definire in che modo si deve comportate lo sfondo in relazione al contenitore o al testo. E' fondamentale utilizzare la direttiva con il prefisso `-webkit` [ampiamente supportata]() dai browser e sfruttare la regola standard come regola di ripiego.

* `-webkit-text-fill-color` con il valore di `transparent` permette di mostrare il gradiente applicato allo sfondo mentre `color` fa in modo che il testo abbia un colore di default nel caso le direttive che andiamo ad utilizzare non fossero supportate dal browser.

* `background-image` [^3] con un valore `linear-gradient()` che mi permette di definire il gradiente di colore che vogliamo applicare sul nostro testo.

* definire il contenitore del testo con un valore `display: inline | inline-block` o utilizzare direttamente un contenitore inline tipo `span` in questo modo si evita di prolungare il gradiente su tutta la lunghezza della pagina.

> Consiglio di approfondire una nuova strategia di design per i fogli di stile chiamata "**utility-first**" spiegata molto bene in un [articolo](https://adamwathan.me/css-utility-classes-and-separation-of-concerns) di [@adamwathan](https://twitter.com/adamwathan) uno dei pionieri di questa tecnica.

<h3 id="supporto">Supporto</h3>

In base a quanto definito dal sito [caniuse](https://caniuse.com/#search=-webkit-background-clip) la direttiva `-webkit-background-clip` è utilizzabile nel **96,73%** dei casi con alcune annotazioni particolari:

> Firefox, Chrome and Safari support the unofficial `-webkit-background-clip: text` (*only with prefix*).

I browser Firefox, Safari e Chrome supportano la direttiva solamente con l'utilizzo del prefisso `-webkit`

> Safari does not support `-webkit-background-clip: text;` for `<button>` elements. But you can put `<span>` inside `<button>` to get the same result.

Safari non permette l'utilizzo della direttiva per gli elementi di tipo `button` ma è possibile bypassare questo limite utilizzando un elemento `span` come contenitore del testo interno.

```Html
<!-- Only Safari -->
<button type="button">
    <span class="text-gradient">Click me!</span>
</button>

```

<h3 id="conclusione">Conclusione</h3>

In conclusione, auguro, a voi che leggerete questa pagina, che questo semplice trucco possa migliorare l'aspetto dei vostri siti web e vi permetta di sperimentare grafiche moderne al passo coi tempi. Alle porte del 2020 sembrano adorare l'uso di questi grandienti di colore su sfondi, bottoni e grafiche di ogni genere.

Beh, adesso sapete come fare e come farlo in modo SEO Friendly.

Se vuoi discutere o migliorare questo articolo vieni a trovarmi su <a href="https://github.com/Mindexperiment/diary/blob/master/css-text-gradient.md" target="_blank">[Github]</a>

<h3 id="riferimenti">Riferimenti</h3>

[^1]: Il riferimento MDN per [-webkit-background-clip](https://developer.mozilla.org/en-US/docs/Web/CSS/background-clip)

[^2]: Il riferimento MDN per [-webkit-text-fill-color](https://developer.mozilla.org/en-US/docs/Web/CSS/-webkit-text-fill-color)

[^3]: Il riferimenro MDN per [background-image](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image)
