---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/7-identificazione/identificazione/"}
---

#concetto #progetto #identificazione 

Gli obiettivi di un protocollo d’identificazione sono: 
1. Se le entità in gioco (A e B) sono **fidate**, **B deve poter completare il protocollo di identificazione certo dell’identità di A** 
	-> eliminazione di falsi negativi, riduzione al più possibile di falsi positivi
2. **B non può riutilizzare lo scambio di identificazione con A per impersonare illegittimamente A presso un’altra entità**, ovvero non può trasferire la credibilità ad altri 
	-> ==<mark style="background: #D2B3FFA6;">Transferability</mark>
3. Deve essere **irrilevante la probabilità che un’entità terza C**, che esegue il protocollo **spacciandosi per A**, possa **indurre B a completare** con successo il protocollo accettando l’identità di C come se fosse quella di A 
	-> <mark style="background: #D2B3FFA6;">Impersonation</mark>
4. Tutti gli **obiettivi devono essere validi** anche se si osservano numerose autenticazioni tra A e B e se l’intrusore C è stato coinvolto in protocolli di identificazione con A e B anche in presenza di simultanee sessioni 
	-> <mark style="background: #D2B3FFA6;">se C spia per molto tempo A e B, gli obiettivi devono comunque rimanere saldi</mark>

## Proprietà  

Nella scelta del protocollo di identificazione ci si basa su:
- Tipo di identificazione (unilaterale o reciproca)
- Efficienza
- Overhead della comunicazione e usabilità su reti con disturbo
- Presenza o meno e tipo di una terza parte come **mediatore** dell'identificazione
- Metodo di memorizzazione 

Esistono due differenti modalità per dimostrare l’identità:
- **Identificazione passiva o *debole*** -> unilaterale ma non reciproca
- **Identificazione attiva o *forte*** -> sia unilaterale che reciproca
## Identificazione passiva

> **L’identificazione è detta passiva quando non richiede elaborazioni da parte dell’identificando**. Generalmente consiste nel comunicare il segreto concordato al verificatore in modo da dimostrare la propria identità. 

-> esempio: identificazione **mediante password** 
Questo tipo di identificazione trasmette empre lo stesso dato, che può quindi essere facilmente intercettato -> presuppone che l'utente si fidi ciecamente del sistema
	-> tipicamente le password non vengono mantenute in chiaro in memoria (o database), ma cifrate oppure hash

Per ovviare a questo tipo di attacchi si usa **concatenare alla password un valore casuale (<mark style="background: #D2B3FFA6;">salt</mark>) prima di calcolarne l’hash** (si memorizza quindi l’hash e il salt in chiaro). Questo permette di aumentare la casualità dell’hash, aumentando lo spazio da esplorare per portare a termine l’attacco.
## Identificazione attiva

> L’identificazione viene detta attiva quando l’identificando deve calcolare e comunicare all’identificatore un **dato sempre differente ed imprevedibile** in modo da farsi riconoscere.

Esempi di questo tipo di identificazione sono: 
- [[sicurezza-informazione-M/7-identificazione/One-time password\|One-time password]]
- [[sicurezza-informazione-M/7-identificazione/Protocolli challenge-response\|Protocolli challenge-response]]
- [[sicurezza-informazione-M/7-identificazione/Protocolli zero-knowledge\|Protocolli zero-knowledge]]

