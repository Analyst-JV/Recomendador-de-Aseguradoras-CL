# Recomendador-de-Aseguradoras-CL
# Benchmark y Score de Aseguradoras – Chile

## 1) Contexto del proyecto y objetivos

En Chile existen **22+ compañías de seguros generales** y se registraron **70.000+ accidentes de tránsito en 2024**. Una comparación “bruta” entre compañías puede **sesgar** a favor o en contra de las más grandes; por ello se diseñó una **evaluación justa, ajustada por exposición y calidad de servicio**.
Se creó un **Score de recomendación** usando **media geométrica ponderada** que **balancea dimensiones** clave y entrega:

 **Foco Corporativo**
* **Benchmark comparativo**  con recomendaciones **personalizados** a 3 compañias segun hallazgos.

**Foco Personal**
* **Recomendación de compañía** por **región** y **tipo de vehículo** (automóvil, camioneta, motocicleta).

## 2) Alcance del análisis (qué se analizó)

* **Talleres disponibles por compañía**.
* **Reclamos y cierre** de los mismos en **SERNAC**.
* **Clientes por compañía** (exposición).
* **Tiempo promedio de reparación** por compañía según **tipo** y **nivel de daño** del vehículo.
* **Dashboard** con recomendador según el perfil y análisis general de compañías *(enlace)*.
* **Métricas creadas** *(enlace)*.

## 3) Metodología de Score resumen

* **Score Recomendación (estricto, 0–100):** media **geométrica ponderada** de **Cobertura** (10%), **Tiempo** (40%) e **IEC** (40%), trabajando todo en 0–1.

exige **desempeño balanceado**; un mal indicador **no se compensa** fácilmente con otros altos.

* **IEC (0–100):** combinación compensatoria de **FR**, **CRS** y **RC** (35%/45%/20%).
* **Tiempo (0–100):** puntajes por severidad (**Leve/Mediana/Grave**) vs. benchmarks (promedio = 50), ponderados 20%/30%/50%.
* **Cobertura (0–1):** talleres por 10k clientes (normalización log y centrado en el promedio regional).
* **FR (0–100):** tasa de reclamos vs. min/prom/máx nacional (lineal por tramos, 0–100).
* **CRS (0–100):** mix de resultados SERNAC ponderado (acoge/no procede/no acoge/no responde).
* **RC (0–100):** 100 × (1 – share “no responde”).

---

## 4) Resumen ejecutivo

### Página 1 — “Análisis Comparativo Aseguradoras”

El panel muestra la **distribución de resultados SERNAC por compañía** y un **benchmark de tiempos por severidad**, evidenciando **diferencias operativas** relevantes.

**Hallazgos clave**

* **BCI**: presenta **peores métricas** en la mayoría de los casos.

  * **Tiempos de reparación**: desfavorables.
  * **Reclamos/10 mil clientes**: **3.ª más alta**.
  * **% de reclamos no acogidos**: elevado.
  * **Cobertura regional**: **decepcionante**; aunque es **3.ª** en cantidad total de talleres, **no** se traduce en **tiempos más bajos**.
* **Porvenir, Sudamérica G y Renta Nacional**: **mejor desempeño** en conjunto.

  * **Porvenir**: **Top 3** en **tiempos promedio de reparación** para **automóvil** (independiente de la gravedad).

    * **Experiencia de cliente**: **100% de reclamos acogidos** y **menor tasa de reclamos/10 mil**.
    * **Advertencia**: **muy pocos clientes**, posible **sesgo** del índice de experiencia (aunque esté normalizado); en algunas regiones tiene **solo un taller**.
  * **Sudamérica G**: **mucha cobertura** de talleres **en todas las regiones**; **tiempos promedio de reparación bajos**.

    * En **IEC** los resultados **no son tan favorables**: % **no responde** presente ,(menos del 10% de las compañias analizadas no responden) y **% no acoge** y **tasa/10 mil** **ligeramente superiores** al promedio.
    
* **BPN**: **alta tasa de reclamos** pese a su **pequeño volumen de clientes** (versus líderes como BCI o Sudamérica G).

  * **Resto de indicadores**: **dentro del promedio**.
  * **Cobertura**: **menor cantidad de talleres** a nivel país; **normalizando por clientes** queda **levemente por debajo del promedio**.

### Página 2 — Motor de recomendación

El **recomendador** personaliza por **región** y **tipo de vehículo**, entregando una compañía sugerida con su **SCORE** y **desglose** (IEC, talleres en la región, tiempos por severidad).

* Con **KPIs normalizados por cliente**, **Porvenir** y **Sudamérica G** **destacan en Biobío**: **tasas de reclamos más bajas**, **tiempos competitivos** y **cobertura adecuada** para su base de clientes.

**“Mejores en perfil”**

* **Porvenir**: combina **baja tasa de reclamos**, **IEC alto** y **tiempos consistentes**; lidera el **SCORE** en el ejemplo mostrado.
* **Sudamérica G**: **competitiva** en tasa de reclamos y tiempos; buen **TOP 5** pese a tener **menos clientes** que incumbentes grandes.

---

## 5) KPIs y consideraciones analíticas

### 5.1 Reclamos SERNAC (nivel compañía)

* Varias compañías concentran mayor **“No Acoge / No Procede”**, sugiriendo **fricción** en la experiencia del consumidor.
* Las que **aceptan más** (o **resuelven mejor**) tienden a **descomprimir** el volumen de reclamos y sostener **mejores IEC**.

### 5.2 Tiempos de reparación (por severidad)

* El **tiempo en siniestros graves** es el **gran diferenciador** (cola larga).
* En la curva comparativa se observan **picos** en algunas compañías (p. ej., un **máximo ~70–75 días**), mientras que otras mantienen trayectorias **descendentes hacia 20–30 días**.
* **Consistencia** entre severidades (leve/mediano/grave) **correlaciona** con **SCORE alto**.

### 5.3 Cobertura de talleres

* La métrica **talleres por 10.000 clientes** distingue **capacidad real**: redes más densas por región reducen **colas** y **tiempos**.

### 5.4 Consideraciones de volumen

En **perfiles muy específicos** (región × tipo de vehículo) algunas compañías pueden tener **pocos asegurados**. Para evitar **volatilidad**:

* Aplicar **umbrales de volumen** (mínimo de clientes por perfil).
* Usar **intervalos de confianza/Wilson** para tasas.
* Incorporar **regularización “shrinkage”** hacia el **promedio nacional**.

---

## 6) Recomendaciones

**Porvenir** — Enfocarse en **crecer la base de clientes** apalancando su ventaja: **IEC alto**, **baja tasa de reclamos** y **tiempos consistentes**. Reforzar **marketing de performance** y presencia en **comparadores** con claims verificables. **Mantener RC=100** como promesa de marca. **Ampliar cobertura selectiva** en regiones con 1 taller para sostener el servicio al escalar.

**Sudamérica G** — **Convertir cobertura en velocidad**:

* **Mejorar experiencia de cliente:** asegurar **RC=100** (cero “no responde”) con **SLA de respuesta definido**  y mensajes estandarizados.
* **Revisar reclamos:** segunda revisión de **“no acoge/no procede”** con criterios documentados y checklist para reducir rechazos evitables; objetivo: **tasa de reclamos/10k ≤ promedio**.
* **Gestión proactiva:** seguimiento de cada caso con **notificaciones de hitos** y **canal único de escalamiento** hasta cierre; contacto proactivo ante atrasos.
* **Aprovechar fortalezas:** comunicar **tiempos promedio bajos** y **cobertura Top 3–4** mientras se corrige el frente de reclamos, para reposicionar la marca en “rápida y que responde”.
**

**BCI** — **Shock operativo** en tiempos: peritaje ≤48h, autorización ≤72h y seguimiento proactivo. **Eliminar “no responde”** y reducir **no acoge** con criterios y checklist claros. **Auditar y reconfigurar la red** por **capacidad efectiva** (no solo conteo) y concentrar flujo en talleres que cumplen SLA. 

**Próximos pasos**

* **Aumentar la temporalidad** (más periodos) para robustecer tendencias.
* **Cruzar causas de reclamo**: hoy disponibles a nivel **global**, no **segmentadas por compañía**; incorporar esta dimensión cuando esté **disponible**.
* Mantener el **benchmark** por **región** y **tipo** para asegurar **comparabilidad** justa y accionable.
