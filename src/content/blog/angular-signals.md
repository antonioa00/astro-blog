---
title: "Angular Signals"
description: ""
pubDate: "May 23 2023"
heroImage: ""
---

Una delle novità più interessanti di Angular 16 è sicuramente l'introduzione di un nuovo tipo di primitive reactive: il <b>Signal</b>. <br>

![Signals-Image](https://cdn.builder.io/api/v1/image/assets%2FYJIGb4i01jvw0SRdL5Bt%2F7b8ddad9e3d34bb3ab35771d91e13d4d?format=webp&width=2000)

## Cos'è?

Possiamo immaginare questa nuova feature come un involucro che ricopre un dato, la sua funzione è quella di inviare una notifica (un segnale, appunto) quando il dato cambia. <br>
Come è facile intuire, questa solo in apparenza piccola modifica ha ripercussioni importanti su tutta la struttura della nostra applicazione: implementa ed incentiva la reattività dell'applicazione e potenzia la change detection permettendoci di avere un controllo migliore su cosa il framework deve aggiornare. <br>
[Come qualcuno fa notare](https://twitter.com/youyuxi/status/1628214809631293440?lang=it), questo tipo di primitivi, mancanti in Angular, sono una funzionalità già implementata da tempo in altri framework dove hanno riscosso un discreto successo.

## ZoneJS e Signal

Attualmente, Angular sa grazie a ZoneJS che qualcosa succede nella nostra applicazione, ovvero si accorge di un eventuale cambiamento in alcune espressioni presenti in alcuni componenti. Ogni volta che qualcosa accade, Angular ricontrolla **tutte** le espressioni di **tutti** i componenti e applica i necessari aggiustamenti al DOM. Grazie ai Signal, Angular sarà in grado di accorgersi quale specifica vista di quale specifico componente subisce dei cambiamenti, senza l'ausilio di ZoneJS ma grazie a quest'ultimi che avviseranno il framework. In questo modo, le risposte ai cambiamenti saranno decisamente ridotte rispetto ad ora con un significativo aumento delle performances.

## In pratica

Vediamo adesso le basi dei Signals.

```typescript
const nome = signal("Antonio");

console.log("Il mio nome è: " + nome());
```

Abbiamo appena creato il nostro primo signal! Ma se volessimo aggiornarlo?

```typescript
nome.set("Roberto");
```

Abbiamo appena modificato il nome in Roberto attraverso **set**.

I **Computed signals** sono una tipologia di Signal che dipendono da altri. Definiamone uno:

```typescript
nome = signal("Mario");
cognome = signal("Rossi");

nomecognome = computed(() => nome() + " " + cognome());
```

Chiaramente, i **computed si aggiorneranno se e solo se si aggiornano i signals da cui dipendono**

Infine, abbiamo gli **Effects** ovvero una funzione asincrona che si esegue ogni qualvolta il valore di uno o più signals a cui sono legati cambia.

```typescript
effect(() => {
  console.log(`Il nome corrente è: ${nome}`);
});
```

## Conclusione

Fatta una breve ma importante panoramica su questa novià introdotta, è bene tenere a mente che, almeno stando ad oggi ovvero alla data di pubblicazione, **i Signals non devono essere usati in produzione essendo in developer preview**. Probabilmente bisognerà attendere la prossima versione per un'implementazione completa. Tolto questo, è bene iniziare ad introdurre un concetto che sono sicuro si rivelerà decisamente utile nell'avvenire. <br>
Si consiglia, inoltre, di approfondire con [questo](https://www.youtube.com/watch?v=iA6iyoantuo) video che spiega in maniera efficace la differenza tra quanto sopra illustrato e gli Observables della libreria RXJS.
