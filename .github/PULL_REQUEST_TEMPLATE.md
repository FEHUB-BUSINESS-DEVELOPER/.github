<!--
================================================================================
 Convenciones obligatorias (validadas por workflow `jira-key-check.yml`):

 • Branch name: <type>/FEH-<num>-<descripcion-kebab>
   tipos válidos: feature | fix | chore | hotfix | refactor | docs | test
   ej: feature/FEH-123-router-multi-bd

 • PR title: debe contener FEH-<num>
   ej: "FEH-123 · BE · Router multi-BD para /inventory/available"

 • Estados Jira automáticos (workflow `jira-transition.yml`):
     PR draft           →  En curso
     PR ready for review →  En revisión
     PR merged           →  QA
================================================================================
-->

## 🔗 Jira

- Issue: **FEH-XXX**
<!-- El workflow agrega automáticamente el link clickable cuando detecta el key. -->

## 📝 Resumen

<!-- 1–3 bullets: qué cambia y por qué (NO el cómo). -->
-

## 🛠 Tipo de cambio

- [ ] `feature` — funcionalidad nueva
- [ ] `fix` — corrección de bug
- [ ] `refactor` — reestructura sin cambio funcional
- [ ] `chore` — mantenimiento, deps, configs
- [ ] `hotfix` — fix urgente a producción
- [ ] `docs` — sólo documentación
- [ ] `test` — tests nuevos o ajustes

## 🎯 Cambios

<!-- Bullets puntuales de qué se modificó. -->
-
-

## ✅ Definition of Done

<!-- Copiá el DoD del ticket Jira y marcá lo cumplido. -->
- [ ]
- [ ]

## 🧪 Cómo probar

<!-- Pasos concretos: comandos, URLs, fixtures. Que un reviewer pueda reproducir solo. -->
1.
2.

## 📷 Evidencias

<!--
 BE  → curl outputs, logs relevantes, queries SQL.
 FE  → screenshots/gif del flujo afectado.
 OPS → comandos + output de validación.
-->

## ⚠️ Notas para el reviewer

<!-- Decisiones de diseño, alternativas descartadas, áreas sensibles, dudas. -->

## 🔧 Impacto

- [ ] Cambia API pública / contrato con otros servicios
- [ ] Requiere migración de BD
- [ ] Nuevas variables de entorno (documentadas en `.env.example` y CLAUDE.md)
- [ ] Afecta otros repos de la org (linkear PRs relacionados abajo)
- [ ] Performance / costo

**PRs relacionados:** <!-- ej: FEHUB-BUSINESS-DEVELOPER/Vecna-FrontEnd#42 -->

## 🚦 Checklist antes de mergear

- [ ] Branch sigue patrón `<type>/FEH-XXX-descripción`
- [ ] PR title contiene `FEH-XXX`
- [ ] CI verde (build + tests + lint)
- [ ] Self-review hecho sobre el diff
- [ ] Sin secretos / credenciales en el código
- [ ] Tests existentes pasan; si suma lógica → tests nuevos incluidos
