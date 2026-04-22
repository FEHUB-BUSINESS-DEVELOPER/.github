# Guía de contribución — FEHUB-BUSINESS-DEVELOPER

Todos los repos de la organización siguen estas reglas para integrarse de forma homogénea con Jira (proyecto **FEH**, [tablero](https://feduro.atlassian.net/jira/software/c/projects/FEH/boards/34)).

## 1. Flujo de trabajo

1. Toma un ticket de Jira en el Tablero FEH y asígnatelo.
2. Crea una rama a partir de `main` con el formato:
   ```
   <type>/FEH-<numero>-<descripcion-corta-kebab-case>
   ```
   Tipos válidos: `feature`, `fix`, `chore`, `hotfix`, `refactor`, `docs`, `test`.
   Ejemplos:
   - `feature/FEH-245-enriquecer-get-customers`
   - `fix/FEH-246-provincia-null-sin-mapeo`
   - `refactor/FEH-248-extraer-province-to-warehouse`

   💡 **Atajo**: desde cada ticket de Jira, panel **Development → Create branch**, la app GitHub for Jira rellena automáticamente el nombre.
3. Haz commits siguiendo **Conventional Commits** e incluyendo la key de Jira:
   - `feat(customers): FEH-245 enriquecer GET /customers con region y warehouse`
   - `fix(customers): FEH-246 manejar provincia null sin mapeo`
   - `chore(deps): FEH-250 bump fastapi a 0.115`

   Tipos: `feat`, `fix`, `docs`, `refactor`, `test`, `perf`, `ci`, `build`, `chore`.
4. Abre un Pull Request contra `main` usando el template. El título debe llevar `[FEH-###]` al inicio.
5. Espera al menos una review aprobatoria y que todos los checks pasen.
6. Merge con **squash** (preferentemente) para mantener historia limpia.

## 2. Integración con Jira

### 2.1 Transiciones automáticas del ticket

El workflow reutilizable `jira-transition.yml` mueve el ticket en el Tablero FEH:

| Evento | Estado en Jira |
|---|---|
| PR abierto como draft | `En curso` |
| PR ready for review / abierto sin draft | `En revisión` |
| PR merged a `main` | `QA` |

### 2.2 Validación obligatoria (bloqueante)

El workflow reutilizable `jira-key-check.yml` valida:

- Nombre de rama con formato `<type>/FEH-###-...`.
- Título del PR con `FEH-###`.
- Opcionalmente, cada commit (activar `enforce_commits: true`).

Si falta la key, el PR no puede hacer merge.

### 2.3 Comentario automático en releases

El workflow `jira-release-comment.yml` comenta en cada ticket incluido en un release con el tag y la URL del release.

## 3. Cómo activar la automatización en un repo

### 3.1 Opción recomendada — instalación con un clic

1. Ve a tu repo en GitHub → pestaña **Actions**.
2. Clic en **New workflow**.
3. En la sección **"By FEHUB-BUSINESS-DEVELOPER"** elige **"Jira automation (FEH)"**.
4. Clic en **Configure** y luego **Commit changes**. Listo.

Esto crea automáticamente `.github/workflows/jira.yml` con los 3 jobs conectados a los workflows reutilizables de la organización.

### 3.2 Opción manual — copiar el snippet

Si prefieres no usar el template, crea `.github/workflows/jira.yml` con el siguiente contenido (idéntico al template):

```yaml
name: Jira

on:
  pull_request:
    types: [opened, reopened, edited, ready_for_review, closed, synchronize]
  release:
    types: [published]

jobs:
  key-check:
    if: github.event_name == 'pull_request' && github.event.action != 'closed'
    uses: FEHUB-BUSINESS-DEVELOPER/.github/.github/workflows/jira-key-check.yml@main
    with:
      project_key: FEH

  transition:
    if: github.event_name == 'pull_request'
    uses: FEHUB-BUSINESS-DEVELOPER/.github/.github/workflows/jira-transition.yml@main
    with:
      project_key: FEH
    secrets:
      JIRA_BASE_URL: ${{ secrets.JIRA_BASE_URL }}
      JIRA_USER_EMAIL: ${{ secrets.JIRA_USER_EMAIL }}
      JIRA_API_TOKEN: ${{ secrets.JIRA_API_TOKEN }}

  release-comment:
    if: github.event_name == 'release'
    uses: FEHUB-BUSINESS-DEVELOPER/.github/.github/workflows/jira-release-comment.yml@main
    with:
      project_key: FEH
    secrets:
      JIRA_BASE_URL: ${{ secrets.JIRA_BASE_URL }}
      JIRA_USER_EMAIL: ${{ secrets.JIRA_USER_EMAIL }}
      JIRA_API_TOKEN: ${{ secrets.JIRA_API_TOKEN }}
```

## 4. Smart Commits

La app **GitHub for Jira** ya instalada en la organización interpreta comandos dentro del mensaje del commit:

| Comando | Efecto |
|---|---|
| `FEH-123 #comment Texto` | Añade un comentario al ticket FEH-123 |
| `FEH-123 #time 2h Avance` | Registra 2h de trabajo (worklog) |
| `FEH-123 #done` | Intenta transicionar el ticket a "Done" (úsalo con criterio) |

Ejemplo de commit combinado:

```
feat(customers): FEH-245 enriquecer GET /customers

FEH-245 #time 3h Implementación del mapeo region/warehouse y tests
```

## 5. Secrets requeridos (a nivel organización — ya configurados)

- `JIRA_BASE_URL` = `https://feduro.atlassian.net`
- `JIRA_USER_EMAIL` = correo Atlassian del bot o usuario de servicio
- `JIRA_API_TOKEN` = token de API creado en `https://id.atlassian.com/manage-profile/security/api-tokens`

## 6. Estilo de código

- Python: `ruff` + `black` + tests con `pytest`.
- JavaScript / TypeScript: `eslint` + `prettier` + tests con `jest` o `vitest`.
- Java: formato estándar del proyecto + `junit`.

## 7. Seguridad

- Nunca subir credenciales, tokens o archivos con datos sensibles.
- Los secrets solo se consumen mediante `secrets.` en Actions.
- Reportar vulnerabilidades según `SECURITY.md`.
