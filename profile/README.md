# Paquete de setup — Organization `FEHUB-BUSINESS-DEVELOPER`

Entregables para completar los pasos 4, 5 y 6 del setup de la org de GitHub.

## Estructura

```
outputs/
├── README.md                          ← este archivo
├── ORG_RULESET.json                   ← Paso 4: ruleset importable
├── RULESET_INSTRUCTIONS.md            ← Paso 4: cómo aplicarlo
├── GITHUB_FOR_JIRA_SETUP.md           ← Paso 5: instalación de la app
├── bowser-fede-backend-ci.yml         ← Paso 6: workflow consumer (rename a ci.yml)
├── bowser-fede-backend-CODEOWNERS     ← Paso 6: CODEOWNERS (rename a CODEOWNERS)
└── BOWSER_PILOT_GUIDE.md              ← Paso 6: guía completa del piloto
```

## Orden de ejecución sugerido

1. **Primero** termina de crear los archivos con Claude Desktop en el repo `.github` (pasos 1-3 ya definidos en el prompt anterior).
2. **Paso 4 — Ruleset:** importa `ORG_RULESET.json` en Organization settings → Rules → Rulesets.
3. **Paso 5 — GitHub for Jira:** sigue `GITHUB_FOR_JIRA_SETUP.md`.
4. **Paso 6 — Piloto Bowser:** sigue `BOWSER_PILOT_GUIDE.md` y usa los dos archivos `bowser-fede-backend-*`.

## Nota sobre dependencia entre pasos

El ruleset requiere que los workflows reutilizables ya existan en el repo `.github/main`, porque los nombres de los status checks (`Lint & Test (Python)`, etc.) se definen ahí. Si aplicas el ruleset **antes** de tener los workflows, los PRs quedarán en "waiting for status" indefinidamente. Por eso el orden: **primero Claude Desktop crea los workflows, luego aplicas el ruleset**.
