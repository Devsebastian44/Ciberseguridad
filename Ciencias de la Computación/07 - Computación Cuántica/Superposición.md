## Conceptos Fundamentales

La **superposición cuántica** permite a un qubit existir en múltiples estados simultáneamente.  
Es el primer "superpoder" de la computación cuántica y la base de su ventaja.

---

## Definición Matemática

Un qubit en superposición se describe como:

[ |\psi⟩ = α|0⟩ + β|1⟩ ]

- α y β son amplitudes complejas
- |α|² → probabilidad de medir |0⟩
- |β|² → probabilidad de medir |1⟩
- Normalización: |α|² + |β|² = 1

---

## Representación Geométrica: Esfera de Bloch

Visualización tridimensional del estado de un qubit.

- **Polo Norte**: |0⟩
- **Polo Sur**: |1⟩
- **Ecuador**: superposición máxima
- **Puntos internos**: estados mixtos (con decoherencia)

[ |\psi⟩ = \cos(\theta/2)|0⟩ + e^{iφ}\sin(\theta/2)|1⟩ ]

- θ: ángulo polar (0 ≤ θ ≤ π)
- φ: ángulo azimutal (0 ≤ φ < 2π)

---

## Creación de Superposición

### Compuerta Hadamard (H)

La más importante para crear superposición.

[ H|0⟩ = \frac{|0⟩ + |1⟩}{\sqrt{2}}, \quad H|1⟩ = \frac{|0⟩ - |1⟩}{\sqrt{2}} ]

Matriz: [ H = \frac{1}{\sqrt{2}} \begin{bmatrix} 1 & 1 \ 1 & -1 \end{bmatrix} ]

---

## Ejemplos Prácticos

### Moneda Cuántica

- Estado inicial: |0⟩ (cara)
- Aplicar H → (|0⟩ + |1⟩)/√2
- Resultado: 50% cara, 50% cruz

### Superposición de n Qubits

- n qubits → representan 2ⁿ estados simultáneamente
- Ejemplo con 3 qubits:  
    |000⟩ + |001⟩ + |010⟩ + |011⟩ + |100⟩ + |101⟩ + |110⟩ + |111⟩

---

## Medición y Colapso

- La medición colapsa el estado cuántico
- Probabilidades determinadas por |amplitud|²
- Proceso irreversible en sistemas ideales

### Bases de Medición

- **Computacional**: {|0⟩, |1⟩}
- **Hadamard**: {|+⟩, |-⟩}
- **Circular**: {|↻⟩, |↺⟩}

---

## Interferencia Cuántica

- **Constructiva**: fases iguales → aumentan probabilidad
- **Destructiva**: fases opuestas → cancelan probabilidad

---

## Aplicaciones de la Superposición

- **Deutsch**: determina funciones en una consulta
- **Grover**: búsqueda más rápida cuadráticamente
- **Transformada de Fourier Cuántica**: base de muchos algoritmos

### Paralelismo Cuántico

- Evaluación simultánea de múltiples entradas
- Exponencial ventaja en problemas específicos

---

## Experimentos Mentales

### El Gato de Schrödinger

- Analogía con el experimento mental clásico
- Ilustra superposición macroscópica
- Señala límites entre mundo cuántico y clásico

---
