# 🔀 Flujo de trabajo Git basado en Git Flow (sin herramienta externa)

Este documento define la estrategia de ramas para el proyecto `indoor-system`, siguiendo el enfoque de **Git Flow manual**, sin necesidad de instalar herramientas externas. El objetivo es mantener una estructura clara, predecible y fácil de integrar en equipos de desarrollo.

---

## 📌 Convenciones de ramas

| Tipo de rama     | Prefijo       | Propósito                                                  |
|------------------|----------------|-------------------------------------------------------------|
| `main`           | —              | Rama estable, lista para producción                         |
| `develop`        | —              | Rama de integración de features y testing                   |
| `feature/*`      | `feature/`     | Desarrollo de nuevas funcionalidades                        |
| `bugfix/*`       | `bugfix/`      | Corrección de errores detectados en `develop`              |
| `hotfix/*`       | `hotfix/`      | Corrección urgente sobre `main`                             |
| `release/*`      | `release/`     | Preparación para nuevos lanzamientos estables              |

---

## 🚀 Flujo de desarrollo habitual

```bash
# 1. Partimos siempre desde develop
git checkout develop

# 2. Creamos una rama de feature
git checkout -b feature/nombre-corto-descriptivo

# 3. Trabajamos normalmente en la rama
# (agregamos cambios, comiteamos, etc.)
git add .
git commit -m "feat(módulo): breve descripción del cambio"

# 4. Subimos la rama al remoto
git push origin feature/nombre-corto-descriptivo

# 5. Cuando finaliza la feature, hacemos merge a develop
git checkout develop
git pull
git merge feature/nombre-corto-descriptivo

# 6. Eliminamos la rama si ya no se usará
git branch -d feature/nombre-corto-descriptivo
git push origin --delete feature/nombre-corto-descriptivo
```

---

## ✅ Buenas prácticas

- Usar **nombres descriptivos y concisos** para las ramas.
- Aplicar **commits semánticos** según la convención:
  - `feat`: nueva funcionalidad
  - `fix`: corrección de error
  - `docs`: cambios en documentación
  - `refactor`: mejora del código sin cambio funcional
  - `test`: agregados o cambios en tests
  - `chore`: tareas menores o mantenimiento
- Incluir el **nombre del módulo o área** afectada en el mensaje de commit entre paréntesis.
  - Ejemplo: `feat(api): agrega endpoint de lectura de sensores`
- Mantener los PR (pull requests) o revisiones simples, con un solo objetivo por rama.

---

## 📁 Ubicación recomendada

Este archivo debe guardarse como parte de la documentación del repositorio en:

```
/docs/git-workflow.md
```

Forma parte del set de documentos base del proyecto para garantizar una colaboración consistente y ordenada.

