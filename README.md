# 🔧 Taller Mecánico Don Ramiro — Solución con Spec-Driven Development (SDD)

Este repositorio contiene el diseño, especificación e implementación de una aplicación web progresiva (PWA) para el **Taller de Don Ramiro**, desarrollada aplicando la metodología **Spec-Driven Development (SDD)**.

🔗 **[Ver Demo Interactiva en Vivo (GitHub Pages)](https://TU-USUARIO.github.io/TU-REPOSITORIO/)**

---

## 📋 Contexto del Problema

Don Ramiro tiene un taller con cuatro mecánicos que solo usan el celular, casi siempre con las manos sucias o engrasadas. 
1. **Interrupciones constantes:** Los clientes llaman varias veces al día para preguntar si su coche está listo, deteniendo el trabajo.
2. **Cuellos de botella y disputas en reparaciones extra:** Cuando aparece una reparación adicional, el trabajo se frena hasta que el cliente aprueba el costo por teléfono (lo que puede tardar días), y en ocasiones el cliente luego niega haber autorizado dicho cobro.
3. **Restricción de alcance:** No se requiere control de inventario, ya que se gestiona actualmente en Excel.

---

## 🗂️ Estructura del Proyecto y Entregables de la Tarea

El repositorio está organizado siguiendo la arquitectura de **Spec-Driven Development**, separando el contexto del agente, las especificaciones verificables, las skills de diseño y la implementación:

```text
taller-don-ramiro-pwa/
├── AGENTS.md                                  # 1. Contexto Persistente del Agente
├── specs/
│   └── 01-aprobacion-cotizacion-extra.spec.md # 2. Especificación del Feature Principal (CA-01 a CA-05)
├── .agents/
│   └── skills/
│       └── brand-design-system/
│           └── SKILL.md                       # 3. Skill de Diseño de Marca ("Fierro & Confianza")
├── index.html                                 # 4. Implementación Funcional (React + Tailwind)
└── README.md                                  # Documentación general de la entrega
