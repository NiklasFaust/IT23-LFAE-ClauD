# 📖 Glossar: LLM-Architektur & Funktionsweise

_Für Anwendungsentwickler_

## 1. Datenstrukturen & Input

### **Token**

Die kleinste Verarbeitungseinheit eines LLMs. Ein Token ist nicht zwingend ein Wort, sondern ein häufig vorkommendes Zeichenfragment.

- **Technisch:** Ein Integer (eine Zahl), der auf einen Eintrag im Vokabular (Dictionary) zeigt.
    
- **Beispiel:** "Informatik" $\rightarrow$ `[Infor, matik]` $\rightarrow$ `[ID: 4812, ID: 110]` (abhängig vom Tokenizer).
    

### **BPE (Byte-Pair Encoding)**

Der Algorithmus, der Text in Tokens zerlegt. Er arbeitet statistisch und fasst häufige Buchstabenpaare iterativ zusammen, bis ein festgelegtes Vokabularlimit erreicht ist.

- **Dev-Note:** Dies ist der Grund, warum LLMs bei seltenen Wörtern oder beim Rechnen (Zahlenzerlegung) Fehler machen.
    

### **Embedding (Einbettung)**

Die Umwandlung eines diskreten Tokens (Integer) in eine kontinuierliche Repräsentation (Vektor).

- **Technisch:** Ein Array von Gleitkommazahlen (Floats), z.B. `[0.12, -0.98, 0.05, ...]`.
    
- **Zweck:** Semantische Bedeutung wird in geometrische Nähe übersetzt. Ähnliche Wörter haben im Vektorraum eine hohe Kosinus-Ähnlichkeit (zeigen in eine ähnliche Richtung).
    

### **Context Window (Kontextfenster)**

Die maximale Anzahl an Tokens, die das Modell gleichzeitig im "Arbeitsspeicher" halten kann (Input + bisher generierter Output).

- **Analogie:** Wie der RAM oder Buffer-Size. Wenn der Text länger ist als das Fenster, wird der Anfang "abgeschnitten" und vergessen.
    

---

## 2. Architektur (Der Transformer)

### **Transformer**

Die neuronale Netzwerkarchitektur, auf der alle modernen LLMs (GPT, Llama, Claude) basieren.

- **Unterschied zu früher:** Verarbeitet Input-Daten **parallel** (nicht sequenziell wie RNNs), was massives Scaling auf GPUs ermöglicht.
    

### **Attention (Self-Attention)**

Der Kernmechanismus des Transformers. Er berechnet die Beziehung jedes Tokens zu jedem anderen Token im Input.

- **Funktion:** Ermöglicht dem Modell, Kontext zu verstehen (z.B. worauf sich "es" oder "sie" in einem Satz bezieht).
    
- **Q / K / V (Query, Key, Value):** Das mathematische Konzept hinter Attention.
    
    - **Query:** Was suche ich? (Die Suchanfrage des aktuellen Tokens).
        
    - **Key:** Was biete ich an? (Die "Tags" oder Schlagworte der anderen Tokens).
        
    - **Value:** Was ist mein Inhalt? (Die Information, die weitergegeben wird, wenn Query und Key matchen).
        

### **Feed-Forward Network (FFN / MLP)**

Eine klassische Schicht neuronaler Netze (Multi-Layer Perceptron), die nach der Attention-Schicht kommt.

- **Funktion:** Verarbeitet die Informationen, die durch Attention gesammelt wurden. Man vermutet, dass hier das "Faktenwissen" gespeichert ist, während Attention eher für das Sprachverständnis/Grammatik zuständig ist.
    

### **Parameter (Gewichte)**

Die einstellbaren Zahlenwerte (Floats) in den Matrizen des neuronalen Netzes.

- **Training:** Diese Werte werden beim Lernen angepasst.
    
- **Inference:** Bei der Nutzung sind diese Werte statisch (read-only).
    
- **Größe:** "7B Modell" bedeutet 7 Milliarden Parameter.
    

---

## 3. Output & Steuerung

### **Logits**

Der "rohe" Output des neuronalen Netzes vor der Wahrscheinlichkeitsberechnung.

- **Technisch:** Ein Vektor mit einer Zahl für jedes mögliche Token im Vokabular. Diese Zahlen können negativ oder beliebig groß sein und sind noch keine Prozentwerte.
    

### **Softmax**

Eine mathematische Funktion, die Logits in Wahrscheinlichkeiten umwandelt.

- **Ergebnis:** Ein Vektor, bei dem alle Werte zwischen 0 und 1 liegen und die Summe exakt 1.0 (100%) ergibt.
    

### **Inference (Inferenz)**

Der Prozess der Anwendung des Modells (im Gegensatz zum Training).

- **Ablauf:** Text rein $\rightarrow$ Forward Pass durch das Netz $\rightarrow$ Wahrscheinlichkeiten für das nächste Token raus.
    

### **Temperature**

Ein Hyperparameter, der die "Kreativität" beim Sampling steuert. Er skaliert die Logits vor dem Softmax.

- **Niedrig (< 0.5):** Die Wahrscheinlichkeitsverteilung wird spitzer. Das Modell wählt fast immer das wahrscheinlichste Wort (deterministisch, gut für Code).
    
- **Hoch (> 1.0):** Die Verteilung wird flacher. Unwahrscheinlichere Wörter erhalten eine Chance ausgewählt zu werden (kreativer, aber chaotischer).
    

### **Top-P (Nucleus Sampling)**

Eine Alternative/Ergänzung zur Temperature.

- **Funktion:** Das Modell betrachtet nur die Top-Tokens, deren Wahrscheinlichkeiten zusammenaddiert den Schwellenwert $P$ (z.B. 0.9) erreichen. Der "lange Schwanz" an unwahrscheinlichen (und oft unsinnigen) Tokens wird abgeschnitten.
    

### **Halluzination**

Wenn das Modell faktisch falsche oder unsinnige Informationen generiert, diese aber rhetorisch überzeugend präsentiert.

- **Ursache:** Das Modell "weiß" nichts, es vervollständigt nur statistische Muster. Wenn ein falsches Muster wahrscheinlicher ist (oder durch hohe Temperature gewählt wird), wird es ausgegeben. Das Modell hat kein Konzept von "Wahrheit", nur von "Wahrscheinlichkeit".