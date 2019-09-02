## Tailwind routine. Consigli di sviluppo.

Ho visto un paio di giorni fa un messaggio pubblicato su Twitter da uno sviluppatore che chiedeva consigli su come utilizzare tailwind css al meglio.

Ho iniziato ad utilizzare la metodologia utility-first di tailwind ancora dalla sua versione ***0.7.x*** quando Adam stava ancora sviluppando tutta la logica solida che ora abbiamo la possibilità di utilizzare.

Un buon punto di partenza per capire il concetto di **utility-first** è il [primo articolo](https://adamwathan.me/css-utility-classes-and-separation-of-concerns/) pubblicato sempre da [@adamwatham](https://twitter.com/adamwathan) sul suo sito dove **spiega molto bene il passaggio dalla vecchia logica a questa nuova logica di sviluppo**.

La richiesta che gira su Twitter da parte di [@tanguyantoine](https://twitter.com/tanguyantoine) è molto semplice: "C'è qualcuno che ha esperienze o consigli da condividere su tailwindcss"

Questa pagina del mio diario è dedicata alla descrizione della mia esperienza con questa nuova metodologia.

---

## TL;DR

### Toc

* [Prima](#prima)
* [Durante](#durante)
* [Dopo](#dopo)
* [Consigli](#consigli)
* [Conclusione](#conclusione)
* [Riferimenti](#riferimenti)

<h3 id="prima">Prima</h3>

Confermo di non essere mai stato un grande designer e non ho mai avuto una spiccata attitudine grafica. Infatti, passavo il mio tempo scopiazzando componenti di design che trovato carini all'interno di template online.

Conosco abbastanza bene le regole CSS ma non sarei mai stato in grado di realizzare componenti grafici complessi, ne tanto meno mi sarei mai sognato diventare un super esperto grafico vista la mia scarsa attitudine per la creatività grafica.

Ho sempre avuto una certa *tensione ad approcciare la grafica con i CSS* perchè non trovavo un sistema coerente in grado di soddisfare le mie esigenze da programmatore.

Ho sempre percepito **i fogli di stile** come *un ammasso di regole* buttate giù più o meno a caso e raggruppate in contenitori (le classi) senza una logica ben definita.

<h3 id="durante">Durante</h3>

Poco più di 6 mesi fa, la svolta. Stavo surfando il web come faccio di solito e mi imbatto casualmente in uno sviluppatore, non ricordo neanche più come ci sono arrivato, fatto stà che su [adamwathan.me](https://adamwathan.me/) inizio a conoscere proprio [Adam](https://twitter.com/adamwathan).

Quando trovo i siti di altri programmatori *sono sempre incuriosito delle tecniche che utilizzano*, con cosa costruiscono il loro sito, come è organizzato, la grafica, gli endpoints.. faccio una vera e propria ***analisi ai raggi X***.

Se trovo articoli li leggo sommariamente per capire a grandi linee il grado di competenze con cui mi sto scontrando.

Cavolo, con Adam è stato più facile del previsto. Il suo articolo [Closing in Tailwind CSS v1.0](https://adamwathan.me/journal/2019/03/11/closing-in-on-tailwind-css-v10/) e poi [CSS Utility Classes and "Separation of Concerns"](https://adamwathan.me/css-utility-classes-and-separation-of-concerns/) sulla separazione dei compiti è stato qualcosa che non si vedeva da tempo nel mondo del web.

Una intuizione talmente banale che quasi sembra impossibile che nessuno c'avesse pensato prima.

```CSS

//da questo
.container {
    margin: 0 auto;
    overflow: hidden;
    padding: 0 1em;
    width: 100%;
}

//a questo
.mx-auto {
    margin: 0 auto;
}
.overflow-hidden {
    overflow: hidden;
}
.px-4 {
    padding: 0 1em;
}
.w-full {
    width: 100%;
}

```

Qui vorrei far notare l'**estrema eleganza e semplicità che questa idea** ha al suo interno. E' strabiliante.

Questa nuova intuizione permette di sviluppare un foglio di stile consistente nelle regole, ben limitato nelle dimensioni e perfettamente in grado di adattarsi alla struttura delle pagine HTML.

<h3 id="dopo">Dopo</h3>

Dopo aver provato [TailwindCSS](https://tailwindcss.com/) è cambiato tutto.

C'è tutto quello che prima mancava nel connubio tra HTML e CSS, c'è coesione, c'è pulizia di codice e soprattutto c'è separazione dei compiti.

<span class="font-semibold text-3xl">MA</span>

**siamo ancora all'inizio**, la tecnica non è ancora perfetta.

<h3 id="consigli">Consigli</h3>

Arriviamo, ora, al punto essenziale, quali sono i consigli che si possono dare a un programmatore che sta iniziando ad utilizzare la logica di Tailwind?

#### Aspettare

Il primo grande consiglio è quello di **aspettare**. Aspettare fintanto che non si ha a disposizione una struttura HTML quasi perfetta. La parte di stile dovrebbe essere l'ultimo passo da compiere seguendo una logica di progressive enhancement.

E' vero, applicare le classi agli elementi è facile non costa nulla se non qualche commit ma se vogliamo programmare nel vero senso della parola, il metodo deve essere rigido. Quindi test, sviluppo logiche backend, struttura HTML e per ultimo la grafica.

#### Dimenticare i componenti

Dimenticatevi l'estrazione dei componenti. **Non è ancora il momento di pensare ai componenti**. Applicate tutte le regole necessarie agli elementi HTML per ottenere il risultato grafico che vi serve. 

Sbizzarritevi il più possibile. Avrete bisogno di molto spazio nel vostro editor oltre i canonici 80-120 caratteri ma non preoccupatevi scrivete le vostre regole in linea con gli elementi HTML.

#### Date un ordine coerente alle regole

Trovate un vostro **ordine** quando applicate le regole ad un elemento. In ordine alfabetico, al contrario, prima le regole di struttura poi i colori e poi i fonts. Trovate il vostro ordine e utilizzatelo in modo coerente su tutto il progetto.

Io mio ordine è un po' complicato ma pur sempre un ordine, la logica va dall'esterno dell'elemento fino al contenuto interno:

* Regole di comportamento
* Regole di dimensione
* Margini
* Paddings
* Forma
* Bordi
* Font
* Testo
* Colori

#### Raccogliete le regole in un foglio esterno

Salvate le regole che applicate in un foglio esterno. Mantenere in parallelo un foglio nel quale salvate le regole che applicate agli elementi vi permette di essere consistenti nell'applicazione delle stesse e soprattutto vi fornisce **un punto unico di raccolta** dal quale attingere le regole quando necessario.

Un breve esempio per chiarire, poniamo di dover applicare dello stile ad una struttura di una pagina di autenticazione in linguaggio blade.

```PHP

@extends('layouts.layout')

@section('body')

<div class="min-h-screen bg-yellow-400">
 <section class="w-full sm:w-2/3 md:w-1/2 sm:mx-auto py-16 px-6 bg-white">
  <header class="mb-6">
   <h2 class="mb-2 font-medium text-3xl">{{ __( 'Sign in' ) }}</h2>
   <p class="font-semibold text-2xl"><a href="{{ route( 'website.homepage' ) }}">{{ config( 'app.name' ) }}</a></p>
  </header>

  <p class="mb-4">{{ __( "Don't have a account?" ) }} <a href="{{ route( 'register' ) }}" class="underline">{{ __( 'Create One' ) }}</a></p>

  @include('auth.login-form')

  <p class="mt-4"><a href="{{ route( 'password.request' ) }}" class="underline">{{ __( 'Forgot Password?' ) }}</a></p>
 </section>
</div>

@endsection

```

Possiamo facilmente mantenere le nostre regole su un foglio in formato .md che ci permette di raggruppare in modo univoco le regole applicate.

Nella prima stesura si capisce chiaramente che alcuni elementi hanno un mix di regole applicate e probabilmente dovranno essere riviste in un ottica più specifica.

```MD
// style.md
div
 min-h-screen bg-yellow-400

section
 w-full sm:w-2/3 md:w-1/2 sm:mx-auto py-16 px-6 bg-white

header
 mb-6

h2
 mb-2 font-medium text-3xl

a
 underline

p
 font-semibold text-2xl

p
 mb-4

p
 mt-4

```

La rivisitazione del nostro foglio .md potrebbe risultare simile al seguente foglio .md nel quale andiamo a descrivere gli elementi specifici utilizzando un meta-linguaggio simile alle classi css. Di queste regole probabilmente alcune non diventeranno mai un componente mentre altre potranno essere riscritte come componente tailwind.

```MD
// style.md
header
 mb-6

h2
 mb-2 font-medium text-3xl

a
 underline

p
 mb-4

section.centered-container
 w-full sm:w-2/3 md:w-1/2 sm:mx-auto py-16 px-6 bg-white

div.full-page-container
 min-h-screen bg-yellow-400

p.subtitle
 font-semibold text-2xl

p.last-item
 mt-4

```

E' importante capire che il mantenimento di un foglio separato con le regole univoche ha la funzione di "repository" per tutto lo stile applicato nella vostra piattaforma, fornendo un punto comune di condivisione e velocizzando l'applicazione delle regole in modo coerente.

Un piccolo esempio di questo foglio di repository leggermente più complesso dei precedenti

```MD
// style.md
section
 py-16 px-6

header
 mb-6

h2
 mb-2 font-medium text-3xl

h3
 mb-4 font-medium text-2xl

h4
 m4-4 italic text-2xl

a
 underline text-teal-600

p.brand-name
 font-semibold text-2xl

## forms
fieldset
 mb-8 p-4 border border-transparent

legend
 p-2 font-light italic

div.input-wrapper
 mb-4

label
 block mb-2 font-bold

input
 appearance-none w-full py-2 px-4 rounded border-2 border-transparent leading-tight

select
 appearance-none outline-none cursor-pointer block w-full py-2 px-4 border-2 border-transparent leading-tight

button
 select-none cursor-pointer inline-block white-space-no-wrap py-2 px-4 rounded border border-transparent leading-tight text-center

## tables
table.full-width
 relative overflow-hidden w-full

th
 p-2 font-semibold text-left

## alert
div.wrapper
 my-4 p-2 font-light

p.title
 mb-4 font-medium

```

#### Estrazione dei componenti

Una volta che il vostro foglio di repository è pieno di regole avete la possibilità di **estrarre tutti i componenti** che saranno necessari nella vostra applicazione.

<h3 id="conclusione">Conclusione</h3>

Concludo semplicemente ricordandovi che potete contribuire, discutere o migliorare questo articolo su [Github](https://github.com/Mindexperiment/diary/blob/master/css-text-gradient.md).

Spero che i consigli contenuti in questa pagina del mio diario vi possano tornare utili nel corso delle vostre sessioni di sviluppo.
