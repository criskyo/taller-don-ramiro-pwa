---
name: brand-design-system-don-ramiro
description: Sistema de diseño y guía de identidad de marca para la aplicación del Taller Mecánico Don Ramiro. Úsala siempre que se creen o modifiquen componentes visuales, vistas o estilos CSS/Tailwind.
---

# Brand & UI Skill: Taller Don Ramiro ("Fierro & Confianza")

## 1. Personalidad de la Marca
- **Para el mecánico:** Herramienta industrial pesada (como una llave de impacto Milwaukee o DeWalt). Directa, indestructible, sin adornos, ultra legible.
- **Para el cliente:** Taller honesto, transparente y ordenado. Transmite seguridad legal y claridad en los precios.

## 2. Paleta de Colores (Tokens de Tailwind)
- **Fondo Mecánico (Modo Oscuro Industrial - evita reflejos y disimula manchas):** `bg-slate-950` (#020617) con tarjetas en `bg-slate-900` (#0f172a) y bordes `border-slate-700`.
- **Fondo Cliente (Modo Claro Confianza):** `bg-slate-50` (#f8fafc) con tarjetas blancas `bg-white` y bordes `border-slate-200`.
- **Acento Primario (Amarillo Seguridad / Taller):** `bg-amber-500` (#f59e0b) con texto negro `text-slate-950` en negrita extrema para botones de acción del mecánico.
- **Semántica de Estados:**
  - `Esperando Aprobación`: `bg-amber-500/20 text-amber-400 border-amber-500` (Alerta activa).
  - `Aprobado / En Reparación`: `bg-emerald-600 text-white` (Éxito rotundo y respaldo).
  - `Rechazado`: `bg-red-600 text-white` (Peligro/Detenido).

## 3. Tipografía y Jerarquía
- **Fuente Principal:** Sans-serif geométrica robusta (`Inter` o `system-ui`).
- **Precios, Placas y Códigos:** Fuente Monoespaciada (`JetBrains Mono` o `font-mono`) en `font-black` y tamaño mínimo `text-2xl` para evitar confusiones numéricas.
- **Prohibido usar texto pequeño:** Ningún texto operativo en la vista del mecánico puede ser menor a `text-lg` (18px).

## 4. Reglas de Componentes Físicos
1. **Botones Táctiles ("Guante/Grasa"):** `min-h-[64px] px-6 rounded-xl font-bold text-lg active:scale-95 transition-transform shadow-lg`.
2. **Placas de Vehículos:** Estilizar siempre como una matrícula física (fondo amarillo o blanco con borde negro doble `border-2 border-slate-900 font-mono uppercase tracking-widest px-3 py-1 rounded`).
3. **Sello de Auditoría Legal:** Mostrar siempre en un bloque tipo recibo bancario con fuente monoespaciada, borde punteado (`border-dashed`) e ícono de escudo de verificación.