# SPEC-001: Flujo de Cotización Adicional y Aprobación Inmutable

## 1. Definición del Problema
Cuando un mecánico descubre una falla adicional al revisar un vehículo, el trabajo se detiene hasta localizar al cliente por teléfono. Esto genera tiempos muertos de hasta varios días. Además, las aprobaciones verbales telefónicas carecen de respaldo, provocando disputas económicas cuando el cliente afirma al recoger el vehículo que nunca autorizó dicho costo.

## 2. Diseño de la Solución
Flujo asíncrono de dos vistas conectadas por un enlace único:
1. **Emisión (Vista Mecánico):** Un formulario de una sola pantalla operable con un dedo (cámara + nota de voz/transcripción automática + teclado numérico gigante para el monto). Al guardar, el estado del vehículo cambia automáticamente a `Esperando Aprobación` y genera un enlace único de WhatsApp.
2. **Resolución y Evidencia (Vista Cliente):** Una tarjeta de resumen que muestra foto del daño, descripción, precio total de la reparación extra y un lienzo táctil (Canvas) o casilla de verificación legal. Al confirmar, se bloquea la cotización en modo solo-lectura, se guarda la huella digital de auditoría (Fecha/Hora, IP, Dispositivo y Firma) y el vehículo pasa automáticamente a `En Reparación`.

## 3. Criterios de Aceptación Verificables (Gherkin / BDD)

- **CA-01 (Usabilidad Manos Sucias en Creación):** 
  DADO que el mecánico está en la pantalla de "Nueva Reparación Adicional", CUANDO ingresa la evidencia y el costo, ENTONCES todos los botones de acción deben medir al menos `64px` de alto y permitir completar el flujo usando únicamente captura de foto, dictado por voz (o tags predefinidos de 1 toque) y un pad numérico en pantalla, sin invocar el teclado de texto estándar del sistema.

- **CA-02 (Bloqueo Automático de Estado):** 
  DADO que un vehículo está en estado `En Revisión`, CUANDO el mecánico envía una cotización adicional, ENTONCES el estado de la orden debe cambiar automáticamente a `Esperando Aprobación` y generar una URL única con token para compartir por WhatsApp.

- **CA-03 (Validación de Aprobación Explícita):** 
  DADO que el cliente abre el enlace único de su cotización pendiente, CUANDO intenta presionar el botón "Aprobar Reparación ($Monto)", ENTONCES el botón debe permanecer deshabilitado hasta que el cliente dibuje su firma en el recuadro táctil (o marque la casilla de aceptación expresa e ingrese los últimos 4 dígitos de su teléfono).

- **CA-04 (Registro de Auditoría Inmutable):** 
  DADO que el cliente aprueba o rechaza la cotización adicional, CUANDO se procesa la acción, ENTONCES el sistema debe almacenar un objeto de auditoría inalterable que contenga: `quote_id`, `status` (APROBADO/RECHAZADO), `timestamp` exacto en formato UTC/local, `client_ip`, `user_agent` y la imagen base64 de la firma, impidiendo cualquier modificación posterior a esa cotización.

- **CA-05 (Comprobante Descargable / Visible):** 
  DADO que una cotización ya fue aprobada, CUANDO el cliente o Don Ramiro vuelven a abrir el enlace, ENTONCES deben visualizar el sello "APROBADO", la evidencia original y los metadatos del registro legal (fecha, hora y firma) en modo de solo lectura.