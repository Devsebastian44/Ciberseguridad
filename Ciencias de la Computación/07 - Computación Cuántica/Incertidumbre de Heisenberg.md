## Principio de Incertidumbre de Heisenberg

El principio de incertidumbre establece límites fundamentales sobre qué tan precisamente podemos conocer pares de propiedades cuánticas simultáneamente.

---

## Formulación Matemática

### Relación general

Relación de Incertidumbre General

- Para dos observables A y B:

```
ΔA · ΔB ≥ ½|⟨[A,B]⟩|
```

- Incertidumbre Posición-Momento

```
Δx · Δp ≥ ℏ/2
```

- Incertidumbre Energía-Tiempo

```
ΔE · Δt ≥ ℏ/2
```

### Casos particulares

- Posición-momento: (\Delta x \cdot \Delta p \geq \hbar/2)
- Energía-tiempo: (\Delta E \cdot \Delta t \geq \hbar/2)

---

## Incertidumbre en Qubits

### Observables complementarios

- **Base Z**: {|0⟩, |1⟩}
- **Base X**: {|+⟩, |-⟩}
- **Base Y**: {|↻⟩, |↺⟩}

### Relaciones

```
ΔX · ΔZ ≥ |⟨Y⟩|/2

ΔY · ΔZ ≥ |⟨X⟩|/2

ΔX · ΔY ≥ |⟨Z⟩|/2
```

---

## Fuentes de Incertidumbre Cuántica

### Fundamental

- Inherente a la naturaleza cuántica
- No puede eliminarse con mejores experimentos

### De preparación

- Conocimiento incompleto del estado
- Reducible con mejor preparación
- Relacionada con la entropía de von Neumann

---

## Ruido Cuántico

### Tipos

1. Ruido de amplitud → pérdida de energía
2. Ruido de fase → pérdida de coherencia
3. Ruido de despolarización → pérdida general de información

### Canales ruidosos

- **Despolarización**:  

 ```
 ε(ρ) = (1-p)ρ + p(I/2)
 ```

- **Amortiguación de amplitud**:  

```
ε(ρ) = A₀ρA₀† + A₁ρA₁†
```

---

## Caracterización del Ruido

- **Tomografía de procesos cuánticos**: reconstrucción de la matriz χ
- **Benchmarking cuántico**:
    - Randomized Benchmarking
    - Gate Set Tomography
    - Cross-Entropy Benchmarking

---

## Mitigación del Ruido

### Supresión

1. Zero-Noise Extrapolation
2. Probabilistic Error Cancellation
3. Symmetry Verification

### Corrección de errores

- Códigos de superficie
- Códigos CSS
- Códigos de color

---

## Aplicaciones de la Incertidumbre

### Generación de números aleatorios

- Aleatoriedad cuántica certificada
- Uso en criptografía

### Sensores cuánticos

- Límite de Heisenberg en sensado
- Mejora cuadrática sobre límite clásico
- Aplicaciones en metrología

---

## Protocolo de Sensado Cuántico

1. Preparación del estado inicial
2. Evolución con el campo a medir
3. Medición para extraer información
4. Estimación mediante procesamiento de datos

### Límites de precisión

- Estándar cuántico
- Heisenberg
---

## Computación Cuántica Tolerante a Fallas

### Umbrales de error

- Códigos de superficie: ~1%
- Códigos concatenados: ~10⁻⁴

### Compiladores cuánticos

- Optimización de circuitos
- Mapeo a hardware específico
- Minimización de errores

---
