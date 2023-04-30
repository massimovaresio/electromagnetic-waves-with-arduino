# electromagnetic-waves-with-arduino
In questo progetto utilizzeremo una scheda Arduino Uno e un dispositivo chiamato fototransistor per studiare le onde elettromagnetiche, in particolar modo quelle della luce visibile. Esploreremo alcune delle applicazioni di rilevamento e misurazione della luce e anche tecnologie di comunicazione e radar.

## Premessa
Ho realizzato questo progetto nell'ambito di una relazione presentata al corso di **Tecnico e sistemista di reti** che ho frequentato presso il centro [Enaip Piemonte di Cuneo](https://www.enaip.piemonte.it/page/corsi/corso/TECNICO-SISTEMISTA-DI-RETI__23378____.html) (Italia). Ho seguito questo corso di specializzazione professionale principalmente per acquisire competenze sull'_hardware_ e sui processi connessi, e per integrare queste competenze a quelle in ambito di _web design_ già in parte maturate nel corso dell'esperienza lavorativa.

## Sintesi del progetto
Il progetto si divide in due esperimenti.
1. **Sensore di luminosità**: nel primo esperimento utilizzeremo un fototransistor come sensore per misurare l'intensità della luce. Inizieremo costruendo un circuito base per un sensore di luce analogico. Utilizzeremo il sensore per misurare la luce ambientale nella stanza ed esploreremo come il valore analogico emesso dalla scheda Arduino UNO R3 sia correlato alla luminosità della luce nella stanza. Poi esamineremo come viene utilizzata la luce nelle **fibre ottiche** per comunicare grandi quantità di informazioni ad alta velocità. Sebbene non si utilizzerà un cavo a fibre ottiche in questa attività, potremo comunque vedere il principio di base di come un trasmettitore invia informazioni attraverso le onde luminose a un ricevitore che le rileva e ne interpreta le informazioni.
2. **Radar di onde luminose**: nella seconda parte dell'esperimento utilizzeremo il sensore di luce come un radar che mappa l'intensità della luce della stanza, collegando il fototransistor ad un servo motore che viene controllato manualmente usando i comandi immessi attraverso il monitor seriale dell'IDE Arduino.

Entrambi gli esperimenti sono stati realizzati in parte utilizzando le guide e le risorse messe a disposizione dall'[Arduino Student Kit](https://www.arduino.cc/education/student-kit), un programma di studio per imparare l'elettronica e le basi di programmazione, progettato specificamente per l'istruzione domestica e l'apprendimento a distanza.

Il codice sviluppato e utilizzato per il progetto è interamente disponibile nella cartella `arduino_code` ed è suddiviso in due parti: `sketch_electromagneticWaveRadar`; `sketch_electromagneticWaveRadar_withServoMotor`.

## Parte 1 - Sensore di luminosità
Il sensore di luce è uno dei sensori più comunemente utilizzato oggigiorno. I telefoni cellulari hanno, ad esempio, sensori di luce che vengono utilizzati dalla fotocamera, per sapere se attivare o meno il flash, quando scattiamo una foto. I lampioni, le luci delle automobili e le luci nei giardini comunali, sono spesso dotati di sensori, che accendono le luci al tramonto. I sistemi di sicurezza utilizzano spesso sensori di luce per modificare le impostazioni di sicurezza durante la notte. Naturalmente, ci sono diversi tipi di sensori di luce. Alcuni rilevano la luminosità, mentre altri rilevano il colore. Diversi tipi di sensori rilevano anche diversi tipi di luce, come ultravioletti, infrarossi e raggi X. In questa attività, costruiremo un sensore di luce analogico, utilizzando una scheda Arduino UNO R3 e un fototransistor, per misurare l'intensità della luce nella stanza.

### Componenti necessari
- 1 scheda elettronica Arduino UNO R3
- 1 fototransistor
- 1 resistenza da 10K Ohm
- 1 resistenza da 220 Ohm
- 1 LED
- 2 cavetti jumper femmina-maschio
- 2 cavi di alimentazione (rosso/nero)
- 6 cavetti jumper

Un **fototransistor** è un componente elettronico che converte l'energia della luce in energia elettrica. In un certo senso, lavora in modo opposto ad un LED. Un LED, infatti, converte l'energia elettrica in energia luminosa. Quando gli elettroni fluiscono, vengono emesse particelle di luce chiamate fotoni e viene prodotta la luce. Se questo processo viene invertito, il LED diventa un fotodiodo e può essere utilizzato per rilevare la luce. Quando la luce lo colpisce, l'energia luminosa viene convertita in energia elettrica e viene prodotto un certo ammontare di corrente. Il problema però, è che la corrente prodotta da un fotodiodo è solitamente molto debole. Tuttavia, se si combina il fotodiodo con un transistor, si può amplificare la corrente e renderla utile per il circuito.

![fototransistor.](assets/images/)
<sub>Fonte immagine: [Arduino Student Kit](https://www.arduino.cc/education/student-kit).</sub>

### Schema elettrico
![schema-elettrico-1.](assets/images/)
<sub>Fonte immagine: [Arduino Student Kit](https://www.arduino.cc/education/student-kit).</sub>

![schema-elettrico-2.](assets/images/)
<sub>Fonte immagine: [Arduino Student Kit](https://www.arduino.cc/education/student-kit).</sub>

Circuito costruito.

![circuito-1.](assets/images/)
<sub>Fonte immagine: produzione propria dell'autore.</sub>

### Misurazione della luce
Inizieremo a scrivere il codice che controlla il circuito. Questo primo sketch consentirà di utilizzare il fototransistor come sensore per rilevare la luminosità o l'intensità della luce nella stanza. Per il momento, ci concentreremo solo sulla creazione del codice per il sensore di luce. Successivamente, aggiungeremo il codice per controllare il LED utilizzandolo come sorgente luminosa.

```c++
// nome dei pin della scheda Arduino utilizzati dal circuito
const int sensorPin = A0;
 
// variabili dichiarate
int lightAmount = 0;

void setup() {
  // codice di installazione, eseguito una volta:

  // avvia il monitor seriale
  Serial.begin(9600);
}

void loop() {
  // codice principale, eseguito ripetutamente:

  // legge il sensore di luce e memorizza la misura in una variabile
  lightAmount = analogRead(sensorPin);
  
  // informazioni di output al monitor seriale
  Serial.print("Light Intensity: ");
  Serial.println(lightAmount);
  
  delay(1000);
}

```
![circuito-2.](assets/images/)
<sub>Fonte immagine: produzione propria dell'autore.</sub>

![circuito-3.](assets/images/)
<sub>Fonte immagine: produzione propria dell'autore.</sub>

![screenshot-1.](assets/images/)
<sub>Fonte immagine: produzione propria dell'autore.</sub>

### Comunicazione ad onde luminose
Uno dei maggiori utilizzi delle onde elettromagnetiche è nel campo della comunicazione. Televisori, radio, telefoni cellulari, computer, dispositivi Bluetooth, robot e giocattoli telecomandati sono solo alcuni esempi di dispositivi che inviano e ricevono informazioni attraverso le onde radio. Ma non sono solo le onde radio che vengono utilizzate per la comunicazione. La tecnologia a **fibra ottica**, ad esempio, utilizza la luce per trasmettere grandi quantità di informazioni su lunghe distanze, a velocità molto elevate.
A differenza delle onde radio, che possono viaggiare attraverso l'aria e persino nello spazio, la fibra ottica richiede l'utilizzo di un cavo costituito da sottili fili in vetro o plastica. Un trasmettitore codifica un segnale elettrico e lo converte in impulsi digitali di luce laser. La luce viaggia attraverso il cavo ottico verso un ricevitore all'altra estremità che rileva, decodifica e converte gli impulsi luminosi nuovamente in segnali elettrici.

In questa attività, utilizzeremo un LED e un sensore di luce per simulare l'invio di informazioni attraverso onde luminose. Il LED inserito nel circuito funzionerà come una sorgente luminosa lampeggiante. Puntando il sensore di luce sul LED osserveremo come il sensore reagisce alla luce lampeggiante, correlando questo comportamento alla tecnologia in fibra ottica e alla trasmissione di informazioni attraverso le onde luminose.

All'interno dello sketch utilizzeremo il timer di Arduino per due diverse attività: la prima è quella di accendere e spegnere il LED per un certo periodo di tempo, la seconda è quella di eseguire misurazioni grazie al sensore di luce a determinati intervalli di tempo. Per accendere e spegnere il LED usiamo una variabile che attiva o disattiva il suo stato. Nel `void loop()` eseguiremo due compiti: il primo è quello di creare un trasmettitore che faccia lampeggiare la luce, il secondo è quello di creare un ricevitore che la rilevi. Le porzioni di codice saranno implementate mediante le funzioni `transmitter()` e `receiver()`.

```c++
// nome dei pin della scheda Arduino utilizzati dal circuito
const int sensorPin = A0;
const int LEDPin = 10;
 
// variabili dichiarate
int lightAmount = 0; // memorizza il valore analogico dal sensore di luce
long timerLED = 0;
long timerSensor = 0;
int toggleLED = 0;

void setup() {
  // codice di installazione, eseguito una volta:

  pinMode(LEDPin, OUTPUT);

  // avvia il monitor seriale
  Serial.begin(9600);

}

void loop() {
  // codice principale, eseguito ripetutamente:

  transmitter ();

  receiver ();

}

void transmitter (){
    // codice per la trasmissione di un segnale a intervalli di 4 secondi
    if (millis() >= timerLED + 2000) {
      toggleLED = !toggleLED;
      digitalWrite(LEDPin, toggleLED);
      timerLED = millis();
  }

}

void receiver (){
  // codice per ricevere segnali ogni 1000 millisecondi
  if (millis() >= timerSensor + 1000) {

    // legge il sensore di luce e memorizza la misura in una variabile
    lightAmount = analogRead(sensorPin);

    // informazioni di output al monitor seriale
    Serial.print("Light Intensity: ");
    Serial.println(lightAmount);

    timerSensor = millis();
    
  }
}

```
Attraverso il monitor seriale dell'IDE Arduino possiamo osservare la misurazione del sensore di luce. Puntiamo il sensore di luce verso il LED blu e osserviamo la lettura dal monitor seriale mentre il LED si accende e si spegne. Possiamo notare che avvicinando il sensore (fototransistor) al LED acceso aumenta l'intensità della luce. L'aumento è chiaramente visibile nelle misurazioni sul monitor seriale.

![circuito-4.](assets/images/)
<sub>Fonte immagine: produzione propria dell'autore.</sub>

![screenshot-2.](assets/images/)
<sub>Fonte immagine: produzione propria dell'autore.</sub>

> Un po' di storia... dal telegrafo alla fibra ottica.

Il **telegrafo** fu il primo dispositivo in grado di trasmettere informazioni a lunghe distanze. I telegrafi inviavano messaggi su un filo di rame conduttivo utilizzando il codice Morse. In questo codice, ogni numero e ogni lettera dell'alfabeto sono rappresentati da una serie di punti e trattini. Questi punti e trattini erano trasmessi elettricamente, attraverso il filo, e ricevuti come clic e/o bip audio all'altra estremità.

![codice-morse.](assets/images/)
<sub>Fonte immagine: [Arduino Student Kit](https://www.arduino.cc/education/student-kit).</sub>

La fibra ottica funziona secondo lo stesso principio di base di un telegrafo. Tuttavia, con la fibra ottica, i dati vengono trasferiti con la luce attraverso un cavo costituito da sottili fili di vetro, anziché un segnale elettrico attraverso un filo di rame. Utilizzando questa codifica digitale, anziché il codice Morse, i cavi in fibra ottica possono trasmettere migliaia di telefonate, pagine Web, video, canzoni e qualsiasi media, in pochissimo tempo.

Il circuito appena costruito è molto simile a un sistema a fibra ottica ma con due differenze principali. Innanzitutto, un sistema a fibra ottica utilizza un cavo tra il trasmettitore (LED blu) e il ricevitore (sensore di luce) che impedisce alla luce di disperdersi su lunghe distanze. L'altra grande differenza è che, al fine di trasmettere grandi quantità di dati, il trasmettitore lampeggia molto velocemente, con impulsi diversi, per trasmettere i bit delle informazioni.

> Sai come fa la NASA a misurare la distanza dalla Luna?

La NASA utilizza un sistema simile al circuito appena costruito per misurare la distanza dalla Luna. Nel 1969, quando Neil Armstrong e Buzz Aldrin approdarono sulla Luna lasciarono qualcosa di più delle loro impronte nella polvere lunare. Si lasciarono infatti alle spalle un pannello catarifrangente per un esperimento con raggi laser - fondamentalmente, uno specchio puntato sulla Terra.
Tornati sulla Terra, con un forte laser puntato sullo specchio inviarono impulsi di luce che sfrecciano nello spazio alla velocità della luce. La luce laser si riflette così dallo specchio e ritorna sulla Terra, che viene rilevata dai telescopi. Usando la velocità della luce e il tempo impiegato dall'impulso laser per viaggiare fino alla Luna e ritorno, gli scienziati possono determinare con precisione la distanza tra la Terra e la Luna.

![nasa-luna.](assets/images/)
<sub>Fonte immagine: [Arduino Student Kit](https://www.arduino.cc/education/student-kit).</sub>



 
