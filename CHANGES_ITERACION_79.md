# PhysioSentinel Gait · Iteración 79

Base: V78 limpia.

## 1. Evolución longitudinal con columnas comparativas

- La gráfica de **Evolución de todos los registros** deja de unir sesiones mediante una línea.
- Cada sesión se representa como una **columna independiente**, ordenada por la fecha y hora clínica completa del registro.
- Se muestra el **valor numérico encima de cada columna**.
- El hover identifica fecha/hora, nombre del registro, vista, ayuda técnica y valor.
- En variables firmadas se añade una referencia horizontal en **0** cuando procede.
- Cuando existe una referencia poblacional compatible, sus límites se representan como **líneas horizontales**, no como columnas.
- Se conservan sin cambios Basal, Último, Δ vs basal y Δ vs anterior.

## 2. Detector temporal de rescate V79

Se añade un segundo detector temporal para el caso específico en que:

- el tracking distal contiene información suficiente,
- pero el detector cinemático principal no obtiene una cadena de alternancia publicable.

El rescate:

- utiliza la misma geometría distal pie derecho - pie izquierdo,
- aplica suavizado robusto, banda muerta e **histéresis** para evitar múltiples cruces falsos,
- exige separación temporal plausible entre alternancias,
- rechaza intervalos manifiestamente incompatibles,
- comprueba periodicidad de forma independiente mediante autocorrelación,
- publica como máximo calidad **Moderada**; nunca se promociona a calidad Alta.

El rescate puede recuperar **cadencia, CV temporal, asimetría temporal y consistencia paso a paso** cuando existe periodicidad suficiente.

### Salvaguarda metodológica

El detector de rescate **NO inventa contactos iniciales IC, TO, tiempos de apoyo, doble apoyo ni fases de apoyo/oscilación**. Si el detector de contacto no supera su QC, esas variables continúan como no calculables.

Se exportan controles internos nuevos:

- `temporal_rescue_attempted`
- `temporal_rescue_used`
- `temporal_rhythm_events`

En Resultados 2D, cuando el rescate ha sido utilizado, aparece una advertencia explícita indicando el origen cinemático de las métricas temporales publicadas.

## 3. Sin cambios en biomecánica

No se modifican fórmulas de ICLM, ICBF, pelvis, tronco, hombros, COM/BOS, rodilla, pie, retropié, sincronización biplanar ni reconstrucción 3D. Se mantienen las convenciones clínicas de signos y las mejoras V76–V78.
