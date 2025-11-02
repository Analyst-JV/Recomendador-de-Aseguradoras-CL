# Metodología de Score(definiciones breves + fórmulas)


## 1) Score  — *(0–100)*

* **Qué es:** media **geométrica ponderada** de Cobertura (10%), Tiempo (40%) e IEC (40%), trabajando todo en 0–1.
* **Por qué importa:** exige **desempeño balanceado**; un factor muy bajo reduce fuertemente el score.

```math
\text{Score} \;=\; 100 \cdot \exp\!\left(\frac{0.10\,\ln c + 0.40\,\ln t + 0.40\,\ln i}{0.10 + 0.40 + 0.40}\right),
\quad c\in[0,1],\; t=\text{Tiempo}/100,\; i=\text{IEC}/100.
```

---

## 2) IEC — *(0–100)*

* **Qué es:** índice compuesto **compensatorio** (calidad y resolución).
* **Por qué importa:** sintetiza señales clave en una sola métrica.

```math
\text{IEC} \;=\; 0.35\,FR \;+\; 0.45\,CRS \;+\; 0.20\,RC
```

---

## 3) CRS Score (Bruto) — *(0–100)*

* **Qué es:** calidad de **resolución** según el mix de resultados.
* **Por qué importa:** premia **acoger**/**resolver**; penaliza **no responder**.

```math
\text{CRS} \;=\; 100 \cdot
\frac{1.00\,s_a \;+\; 0.35\,s_{np} \;+\; 0.20\,s_{na} \;+\; 0\cdot s_{nr}}
{s_a \;+\; s_{np} \;+\; s_{na} \;+\; s_{nr}}
\qquad
\begin{aligned}
&s_a:\ \text{acoge}\\
&s_{np}:\ \text{no procede}\\
&s_{na}:\ \text{no acoge}\\
&s_{nr}:\ \text{no responde}
\end{aligned}
```

---

## 4) FR Score (Bruto) — *(0–100)*

* **Qué es:** desempeño en **tasa de reclamos** frente a benchmarks nacionales.
* **Por qué importa:** proxy de **calidad/posventa** (menos reclamos ⇒ mejor).
  *(Luego acotar a ([0,100])).*

```math
\text{FR}(r) \;=\;
\begin{cases}
50 \;+\; 50\,\dfrac{a-r}{a-m}, & r \le a,\\[8pt]
50 \;-\; 50\,\dfrac{r-a}{M-a}, & r > a,
\end{cases}
\quad
\begin{aligned}
&r:& \text{tasa compañía}\\
&m,a,M:& \text{mín, prom, máx nacionales}
\end{aligned}
```

---

## 5) Tiempo Score (simple • TREATAS) — *(0–100)*

* **Qué es:** desempeño de **tiempos promedio** por severidad vs. benchmarks; pondera más **Grave**.
* **Por qué importa:** la **celeridad** impacta directamente la satisfacción.
  *(Cada (S_s) se acota a ([0,100])).*

```math
S_s(r_s) \;=\;
\begin{cases}
50 \;+\; 50\,\dfrac{a_s-r_s}{a_s-m_s}, & r_s \le a_s,\\[8pt]
50 \;-\; 50\,\dfrac{r_s-a_s}{M_s-a_s}, & r_s > a_s,
\end{cases}
\quad
s\in\{\text{Leve},\text{Mediana},\text{Grave}\}
```

```math
\text{TiempoScore} \;=\; 0.20\,S_{\text{Leve}} \;+\; 0.30\,S_{\text{Mediana}} \;+\; 0.50\,S_{\text{Grave}}
```

---

## 6) Cobertura Territorial — *(0–1)*

* **Qué es:** densidad de talleres por 10k clientes, normalizada en **log** entre mínimo y máximo regional; centra el **promedio** regional en 0.5 (si es válido).
* **Por qué importa:** refleja **acceso** y disponibilidad territorial.
  *(Luego acotar el resultado a ([0,1])).*

```math
y=\frac{\ln v - \ln lo}{\ln hi - \ln lo}, 
\qquad
y_{\text{avg}}=\frac{\ln \overline v - \ln lo}{\ln hi - \ln lo}
```

```math
\text{Cobertura} \;=\;
\begin{cases}
y, & y_{\text{avg}}\notin(0,1),\\[6pt]
0.5\,\dfrac{y}{y_{\text{avg}}}, & y \le y_{\text{avg}},\\[10pt]
0.5 \;+\; 0.5\,\dfrac{y - y_{\text{avg}}}{1 - y_{\text{avg}}}, & y > y_{\text{avg}}.
\end{cases}
```

---

## 7) RC — *(0–100)*

* **Qué es:** cumplimiento de **respuesta** (inverso del “no responde”).
* **Por qué importa:** mide **responsividad** operativa.

```math
\text{RC} \;=\; 100\,\big(1 - s_{nr}\big), \qquad s_{nr}\in[0,1]
```

---

## 8) Share Proveedor no responde — *(0–1)*

* **Qué es:** proporción de casos en que el proveedor **no responde** (por compañía).
* **Por qué importa:** indicador directo de **ausencia de respuesta**.

```math
s_{nr} \;=\;
\begin{cases}
p/100, & \text{si el dato } p \text{ viene en \%},\\[6pt]
p, & \text{si } p \in [0,1],\\[6pt]
0, & \text{si no hay datos}.
\end{cases}
```

---
