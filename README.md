# TRAINING #

## In che cosa consiste la parte di Training? ##

La fase di Training si divide in 2 parti:
1.	Generazione dei file.csv a partire dai file delle tracce utente. Questi file.csv contengono i delta dei vari campi (lon, lat, alt, ecc…) da un punto a quello precedente.
2.	Una volta generati i file.csv, questi vengono dati in pasto al modello vero e proprio tramite l’operazione di training.

## Preparazione dell’applicazione ##
*	Devono essere create le seguenti cartelle:
   
    *	***“mapMatching/UserTrackReady/”***
    *	***“mapMatching/UserTrackTrained/”***
    *	***“mapMatching/machine_learning/ReadyToTraining/”***
    *	***“mapMatching/machine_learning/Trained/”***
    *	***“mapMatching/debug/”***
   
*	Devono essere messe nella cartella “mapMatching/UserTrackReady/” i file contenenti le tracce utente vere e proprie (file .json)
* Deve essere scaricato l'opportuno file delle mappe di Open Street Maps, reperibili nell'apposita cartella OneDrive tramite il percorso WOOLLF/SOFTWARE/mappe_osm .
    * Il nome del file della mappa che si vuole utilizzare deve essere specificato nel file GPSConverter.java .

## Come vengono eseguite queste 2 parti dalla nostra applicazione? ##

Ognuna delle due parti viene eseguita tramite un semplice clic (dunque, un clic per la parte 1, e un clic per la parte 2). Ma vediamo più nel dettaglio:
1.	La prima parte viene eseguita in Java, tramite la classe “***TrainingScheduler.java***”. Questa classe prende uno alla volta i file .json contenuti in “mapMatching/UserTrackReady/”, e il trasforma in file .csv.
    *	I file .json che sono stati dati in pasto al TrainingScheduler vengono poi spostati automaticamente in “mapMatching/UserTrackTrained/”.
    *	I file .csv creati vengono messi automaticamente nella cartella “mapMatching/machine_learning/ReadyToTraining/”.
2.	La seconda parte viene eseguita in python, tramite il file “***training_scheduler.py***”. Questo script prende uno alla volta i file .csv contenuti in “mapMatching/machine_learning/ReadyToTraining/”, e li usa per fare il training del modello.
    *	I file .csv che sono stati quindi utilizzati per il training vengono poi spostati automaticamente in “mapMatching/UserTrackTrained/”.

## Previsione di una traccia utente ##
*	Tramite il file “***Delta.java***” posso generare il file .csv della traccia utente.
*	Tramite il file “***prediction_test.py***” posso generare il file .json contenete la traccia predetta dal modello.

N.B.: attenzione ai nomi dei file di input che sono riportati nel file “prediction_test.py”.

## Parametri ##
TrainingScheduler.java
*	directoryReady: directory che contiene le tracce utente ancora da analizzare.
*	directoryTrained: directory che contiene le tracce utente già analizzate.
*	directoryDebug: directory che contiene informazioni di debug sulle tracce utente analizzate
*	directoryDelta: directory che contiene i file .csv generati dopo il primo step.
*	debug: variabile booleana che indica se bisogna fare o meno il debug delle tracce utente che verranno processate.

TrainingGenerator.java
*	bufferSize: variabile che indica il numero di punti che compongono il buffer
*	roadPortion: variabile che indica la porzione di strada da analizzare alla volta (pezzo per pezzo), espressa come numero di punti della traccia utente.
*	marginMappingUp: variabile che indica quanti punti guardare in avanti per avere un miglior map matching con la strada sottostante.
*	marginMappingDown: variabile che indica quanti punti guardare all’indietro per avere un miglior map matching con la strada sottostante.

GPSConverter.java
*	variabili di normalizzazione dei dati: costanti che vengono utilizzate per la normalizzazione dei dati.
* nome della mappa di Open Street Maps che viene utilizzata.


