<!--
  ⚠️ Formato obligatorio del título del PR:
    [FEH-###] <type>(scope): descripción corta
  Ejemplos:
    [FEH-245] feat(customers): enriquecer GET /customers con region y warehouse
    [FEH-248] refactor(static_data): extraer province_to_warehouse

  ⚠️ Formato obligatorio de la rama:
    <type>/FEH-<numero>-descripcion-corta-en-kebab-case
  Tipos permitidos: feature, fix, chore, hotfix, refactor, docs, test

  El workflow .github/workflows/jira-key-check.yml bloqueará el merge
  si el título o la rama no contienen una key válida del proyecto FEH.
-->

## 🎯 Ticket de Jira

<!-- Reemplaza 000 por el número real del ticket -->
- Jira: [FEH-000](https://feduro.atlassian.net/browse/FEH-000)

## 📋 Descripción

<!-- ¿Qué hace este PR y por qué? -->

## 🧪 Tipo de cambio

- [ ] 🐛 Bug fix (`fix/FEH-###-...`)
- [ ] ✨ Nueva funcionalidad (`feature/FEH-###-...`)
- [ ] 💥 Breaking change
- [ ] 📝 Documentación (`docs/FEH-###-...`)
- [ ] ♻️ Refactor (`refactor/FEH-###-...`)
- [ ] ⚡ Mejora de rendimiento
- [ ] ✅ Tests (`test/FEH-###-...`)
- [ ] 🔧 Configuración / infraestructura (`chore/FEH-###-...`)
- [ ] 🚑 Hotfix (`hotfix/FEH-###-...`)

## ✅ Checklist

- [ ] El título del PR contiene la key de Jira en formato `[FEH-###]`
- [ ] El nombre de la rama sigue la convención `<type>/FEH-###-...`
- [ ] Los commits siguen Conventional Commits e incluyen `FEH-###`
- [ ] He ejecutado los tests localmente y todos pasan
- [ ] He agregado / actualizado tests para cubrir mis cambios
- [ ] He actualizado la documentación si era necesario
- [ ] No introduzco credenciales ni información sensible
- [ ] He probado manualmente el cambio

## 🔁 Transiciones automáticas en Jira

Este PR moverá el ticket en el Tablero FEH automáticamente:

| Evento en GitHub | Estado en Jira |
|---|---|
| PR abierto como **draft** | `En curso` |
| PR marcado **ready for review** | `En revisión` |
| PR **merged** a `main` | `QA` |

## 📸 Evidencias

<!-- Screenshots, videos o logs relevantes -->

## 📝 Notas para el revisor

<!-- Contexto adicional, decisiones de diseño, áreas de riesgo -->
