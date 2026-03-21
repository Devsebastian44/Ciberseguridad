## Introducción al Entrelazamiento Cuántico

El entrelazamiento cuántico es uno de los fenómenos más contraintuitivos y poderosos de la mecánica cuántica.  
Einstein lo llamó _“acción fantasmal a distancia”_ por sus implicaciones aparentemente imposibles.

---

## Definición Formal

El entrelazamiento ocurre cuando dos o más qubits se correlacionan de tal manera que el estado cuántico de cada partícula no puede describirse independientemente.

- **Estado separable**: (|ψ⟩ = |ψ₁⟩ ⊗ |ψ₂⟩)
- **Estado entrelazado**: no puede escribirse como producto tensorial

---

## Estados de Bell

Los cuatro estados entrelazados máximamente para dos qubits:

[ |Φ⁺⟩ = \frac{|00⟩ + |11⟩}{\sqrt{2}}, \quad |Φ⁻⟩ = \frac{|00⟩ - |11⟩}{\sqrt{2}} ]

[ |Ψ⁺⟩ = \frac{|01⟩ + |10⟩}{\sqrt{2}}, \quad |Ψ⁻⟩ = \frac{|01⟩ - |10⟩}{\sqrt{2}} ]

---

## Creación de Entrelazamiento

### Compuerta CNOT

[ CNOT|00⟩ = |00⟩, \quad CNOT|01⟩ = |01⟩ ]  
[ CNOT|10⟩ = |11⟩, \quad CNOT|11⟩ = |10⟩ ]

### Circuito para estado de Bell

1. Aplicar H al primer qubit → ((|0⟩ + |1⟩)/\sqrt{2} ⊗ |0⟩)
2. Aplicar CNOT → ((|00⟩ + |11⟩)/\sqrt{2})

---

## Propiedades del Entrelazamiento

### No-localidad

- Mediciones en un qubit afectan instantáneamente al otro
- Viola desigualdades de Bell
- No permite comunicación superlumínica

### Monogamia

- Un qubit no puede estar máximamente entrelazado con dos qubits
- Base de la seguridad cuántica

---

## Medición de Entrelazamiento

### Entropía de Entrelazamiento

[ E(ρ) = -Tr(ρₐ \log ρₐ) ]

### Concurrencia

[ C(ρ) = \max{0, \sqrt{λ₁} - \sqrt{λ₂} - \sqrt{λ₃} - \sqrt{λ₄}} ]

---

## Aplicaciones

### Teletransportación Cuántica

1. Crear estado de Bell entre Alice y Bob
2. Alice mide en base de Bell
3. Alice comunica resultado clásicamente
4. Bob aplica operación correctiva

### Criptografía Cuántica

- **BB84**: distribución segura de claves
- **E91**: basado en entrelazamiento

### Algoritmos

- **Shor**: factorización
- **Grover**: amplificación de amplitudes
- **Computación distribuida**: entre múltiples procesadores

---

## Entrelazamiento Multipartito

### Estados GHZ

[ |GHZ⟩ = \frac{|000⟩ + |111⟩}{\sqrt{2}} ]

### Estados W

[ |W⟩ = \frac{|001⟩ + |010⟩ + |100⟩}{\sqrt{3}} ]

---

## Desafíos

- **Decoherencia**: interacción con ambiente destruye entrelazamiento
- **Distribución**: pérdidas en canales, necesidad de repetidores cuánticos y redes cuánticas

---

## Experimentos Históricos

- **Aspect (1982)**: primera violación clara de desigualdades de Bell
- **Teletransportación (1997)**: primer experimento exitoso de teletransportación cuántica

---
