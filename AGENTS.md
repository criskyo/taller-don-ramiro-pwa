# Contexto Global del Proyecto: Taller Don Ramiro (PWA)

## 1. Visión del Producto
Aplicación web mobile-first para un taller mecánico de 4 operarios. Su único propósito es eliminar las llamadas de seguimiento de los clientes y formalizar la aprobación rápida de cotizaciones adicionales con respaldo probatorio inmutable.

## 2. Restricciones de Alcance (Out of Scope)
- PROHIBIDO implementar módulos de inventario, stock de repuestos, almacén o compras (Don Ramiro ya lo gestiona en Excel).
- PROHIBIDO exigir registro con usuario/contraseña a los clientes finales (todo acceso de cliente es vía URL firmada con token único).
- PROHIBIDO diseñar vistas pensadas para escritorio (Desktop); el 100% del tráfico es móvil.

## 3. Reglas de UX/UI por Rol
### A. Rol Mecánico ("Hands-Dirty UI")
- Los mecánicos usan el celular con las manos engrasadas o sucias.
- Todos los botones interactivos deben tener una altura mínima de `64px` (`min-h-16`) y separación amplia (`gap-4`) para evitar toques accidentales.
- Prohibido el uso de inputs de texto libre con teclado QWERTY. Usar únicamente: dictado por voz (Web Speech API), cámara directa, selectores de 1 toque y teclado numérico gigante para precios.
- Alto contraste obligatorio para lectura bajo luz solar directa o poca luz en foso mecánico.

### B. Rol Cliente ("Zero-Friction Portal")
- Carga instantánea sin instalación.
- Lenguaje claro, transparente y visual (barra de progreso sencilla y evidencia fotográfica prominente).

## 4. Stack Tecnológico y Convenciones
- **Frontend:** React (Next.js App Router o Vite), TypeScript estricto, Tailwind CSS, Lucide Icons.
- **Estado / Persistencia:** Almacenamiento transaccional con registro de auditoría inmutable (`timestamp` ISO-8601, `ip_address`, `user_agent`, `signature_hash`).
- **Principio SDD:** Ningún componente se codifica sin cumplir los Criterios de Aceptación definidos en `/specs/`.