# SPEC-002: Tablero de Cambio de Estado "One-Tap" y Rastreo en Vivo con Alertas Automáticas

## 1. Definición del Problema
Los clientes (User Persona: *Carolina*) llaman entre 2 y 4 veces al día al taller porque sufren de incertidumbre sobre el avance de su vehículo. Cada llamada obliga a Don Ramiro o a sus 4 mecánicos (User Persona: *"El Chato" Morales*) a detener la reparación, limpiarse las manos engrasadas y contestar el teléfono, perdiendo hasta 2 horas productivas diarias. Además, cuando un coche termina de repararse, a veces pasan horas antes de que alguien tenga tiempo de avisarle al cliente para que pase a recogerlo, ocupando espacio valioso en el taller.

## 2. Diseño de la Solución
Sistema sincronizado de actualización de estados con un solo toque y notificación proactiva sin intervención manual:
1. **Tablero Operativo "One-Tap" (Vista Mecánico):** Tarjetas por vehículo identificadas con placa grande donde el mecánico avanza el estado con **un solo toque** en botones de `>= 64px` (`Recibido` ➔ `En Revisión` ➔ `En Reparación` ➔ `Pruebas / Lavado` ➔ `Listo para Entrega`), sin usar teclado ni redactar mensajes.
2. **Tracker Público en Tiempo Real (Vista Cliente):** Enlace único (sin login) con una barra de progreso visual e historial de horas exactas de cada cambio de etapa, junto con la hora estimada de entrega.
3. **Disparador Automático de Mensajes (Zero-Typing Notifications):** Cada cambio de estado en el tablero del mecánico dispara automáticamente una plantilla preconfigurada por WhatsApp/SMS al cliente, destacando especialmente la alerta de `Listo para Entrega` con el resumen final de cuenta y horario de recogida.

---

## 3. Criterios de Aceptación Verificables (Gherkin / BDD)

- **CA-01 (Actualización One-Tap para Manos Sucias):**
  DADO que el mecánico ("El Chato") visualiza la tarjeta de un vehículo activo en su celular, CUANDO desea actualizar la etapa del vehículo, ENTONCES debe poder cambiar al siguiente estado con un único toque sobre un botón de mínimo `64px` de altura (`min-h-16`) y alto contraste, sin que el sistema despliegue teclados de texto ni cuadros de confirmación adicionales.

- **CA-02 (Sincronización Instantánea en el Portal del Cliente):**
  DADO que el cliente (Carolina) tiene abierto su enlace único de seguimiento, CUANDO el mecánico cambia el estado del vehículo en el taller, ENTONCES la barra de progreso del cliente debe actualizarse reflejando la nueva etapa activa y registrando la hora exacta (`HH:mm`) del cambio en la línea de tiempo del servicio.

- **CA-03 (Disparo Automático de Notificación en Transiciones Clave):**
  DADO que un vehículo cambia su estado a `En Reparación` o a `Listo para Entrega`, CUANDO el sistema guarda el nuevo estado, ENTONCES debe generar y enviar automáticamente el mensaje predefinido de WhatsApp al número del cliente con el enlace al tracker, sin requerir que el mecánico escriba ni copie texto manualmente.

- **CA-04 (Bloqueo de Avance con Cotización Pendiente):**
  DADO que un vehículo se encuentra en estado `Esperando Aprobación` (vinculado a la SPEC-001), CUANDO el mecánico intenta pasarlo manualmente a `Listo para Entrega`, ENTONCES el sistema debe bloquear la transición y mostrar una alerta visual industrial indicando que existe un presupuesto adicional pendiente de firma o rechazo por parte del cliente.

- **CA-05 (Resumen de Cierre en Estado "Listo para Entrega"):**
  DADO que el vehículo alcanza el estado final `Listo para Entrega`, CUANDO el cliente abre su enlace de seguimiento, ENTONCES debe visualizar un banner verde de confirmación, el monto total consolidado a pagar (servicio base + reparaciones adicionales aprobadas en SPEC-001, excluyendo desgloses de inventario interno) y el botón con la ubicación del taller para pasar a recogerlo.

---

## 4. Métricas de Éxito (Product & Business KPIs)

Para validar que este feature no solo "funciona" técnicamente sino que **importa** al negocio de Don Ramiro, se definen métricas divididas en Eficiencia Operativa, Adopción de Usuario e Impacto en Negocio:

### A. Métricas de Impacto Operativo (Dolor Principal)
1. **Reducción de llamadas entrantes de seguimiento (North Star Metric):**
   - **Línea base actual:** ~15 a 20 llamadas diarias preguntando *"¿cómo va mi carro?"*.
   - **Meta de éxito:** Reducción del **80% en llamadas de consulta de estado** (máximo 3 llamadas diarias) tras las primeras 4 semanas de implementación.
2. **Tiempo de rotación de bahía post-reparación (Time-to-Pickup):**
   - **Definición:** Tiempo que transcurre desde que el mecánico termina el arreglo hasta que el cliente se entera y recoge el auto.
   - **Meta de éxito:** Reducir el tiempo muerto de notificación de **3 horas a menos de 1 minuto** gracias al disparo automático del estado `Listo para Entrega`.

### B. Métricas de Usabilidad y Adopción del Mecánico ("El Chato")
3. **Time-on-Task de actualización de estado:**
   - **Definición:** Tiempo promedio que tarda un mecánico con manos sucias desde que desbloquea el celular hasta que actualiza el estado de un coche.
   - **Meta de éxito:** **Menos de 5 segundos por actualización** (validando la eficacia de la interfaz *One-Tap* sin teclado).
4. **Tasa de adopción operativa diaria:**
   - **Definición:** Porcentaje de vehículos ingresados al taller que pasan por al menos 3 actualizaciones de estado digitales durante su estancia.
   - **Meta de éxito:** **>= 90% de los vehículos** actualizados en la app sin intervención telefónica de Don Ramiro.

### C. Métricas de Experiencia del Cliente (Carolina)
5. **Tasa de autoservicio en el Portal de Seguimiento (Self-Service Rate):**
   - **Definición:** Porcentaje de clientes activos que abren su enlace único de seguimiento al menos una vez durante la reparación sin llamar al taller.
   - **Meta de éxito:** **>= 85% de clientes** consultando el progreso vía web link.
