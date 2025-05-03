---

# 📚 Ejemplo completo de flujo Git en este proyecto

Esta sección documenta paso a paso cómo aplicar el flujo Git manual en este proyecto, siguiendo la estrategia `Git Flow` sin herramientas externas.

---

## 🤔 Conceptos clave antes de comenzar

### 🔀 Estructura de ramas

| Rama        | Rol principal                                                                                    |
| ----------- | ------------------------------------------------------------------------------------------------ |
| `develop`   | Rama **activa de desarrollo**. Contiene la integración de todas las features terminadas.         |
| `feature/*` | Rama **temporal** para trabajar en una funcionalidad específica. Se borra al completar el merge. |
| `main`      | Rama **estable para producción**. Solo se actualiza desde `release/*` o `hotfix/*`.              |

### 🚀 Por qué subir una rama `feature/*` al repositorio remoto

* Permite trabajar desde distintos dispositivos o con otros colaboradores.
* Habilita la creación de un **Pull Request** (PR) para revisar el código antes de integrarlo.
* Documenta el proceso de desarrollo con contexto y mensajes claros.
* Aisla los cambios sin afectar `develop` hasta que todo esté listo.

> 🔐 Subir una rama `feature` al remoto **no publica contenido a producción**. Solo versiona el trabajo.

### 👀 Y por qué no pushear directamente a `develop`

* Porque `develop` debería contener solo funcionalidades completas y testeadas.
* Evita conflictos o errores no deseados si alguien más está trabajando sobre esa rama.
* Favorece un flujo ordenado y seguro para equipos de trabajo.

---

## 🧐 Excepciones: ¿Cuándo sí conviene trabajar directamente en `develop`?

En algunos casos, especialmente en documentación o proyectos personales, puede ser más práctico editar directamente sobre `develop`.

### ✅ Situaciones donde es válido:

* Estás trabajando **solo** en el proyecto.
* Es un cambio **rápido y menor**, como corregir errores de ortografía o agregar notas.
* Tenés **confianza en que el cambio no rompe nada**.
* Hiciste `git pull` antes de trabajar para evitar conflictos.

### ⛔️ Cuándo deberías evitarlo:

* Si hay **más personas** en el equipo.
* Si estás modificando **múltiples archivos o estructuras**.
* Si hacés algo que requiere **revisión o prueba**.
* Si estás en una etapa de **preparación para producción** o `release/*`.

> 📚 Regla general: si es pequeño, rápido y claro, podés hacerlo en `develop`. Si es algo que querés poder revisar, testear o deshacer con seguridad, usá una rama `feature/*`.

---

### 📌 ¿Qué es un Pull Request y cómo se hace merge desde la plataforma?

Un **Pull Request (PR)** es una solicitud para fusionar una rama (por ejemplo, `feature/docs-raspberry`) con otra (como `develop`). Se realiza desde la plataforma web del repositorio (ej. GitHub, GitLab, Bitbucket).

Pasos:

1. Subís tu rama con `git push origin feature/nombre`.
2. Vas a la página del repositorio.
3. La plataforma detecta tu rama nueva y propone abrir un PR.
4. Allí podés:

   * Agregar una descripción del cambio.
   * Ver diferencias (diff) entre ramas.
   * Pedir revisión a otro miembro.
   * Hacer comentarios o resolver dudas.
5. Una vez aprobado, hacés clic en "Merge Pull Request".
6. Ahora `develop` tiene tus cambios integrados.

---

## ⏩ Alternativa: Merge rápido a develop desde consola

Si estás trabajando solo o el cambio es menor y ya está testeado, podés hacer el merge directamente sin usar Pull Requests.

```bash
# 1. Asegurate de haber comiteado todo en tu rama actual
# 2. Cambiá a develop y actualizá

git checkout develop
git pull

# 3. Merge de tu rama feature a develop
git merge feature/nombre-de-tu-rama

# 4. Subís develop con el cambio integrado
git push origin develop

# 5. Eliminás la rama feature si ya no se necesita
git branch -d feature/nombre-de-tu-rama
git push origin --delete feature/nombre-de-tu-rama
```

> 🔍 Ideal para casos simples como cambios en documentación, test o scripts. No recomendable para features complejas o trabajo colaborativo.

---

## 📂 Convención para redactar commits

Seguimos la convención semántica: `tipo(módulo): descripción corta en presente`.

### 🔄 Estructura general:

```bash
<tipo>(<módulo>): <descripción corta>
```

### 🔧 Ejemplos

```bash
feat(api): agrega endpoint de lectura de sensores
fix(auth): corrige error en validación de token
docs(raspberry): agrega recomendaciones de uso de 4GB RAM
refactor(frontend): reorganiza estructura de carpetas
test(server): agrega test para controlador de errores
chore(deps): actualiza dependencias de Express
```

### 📘 Tipos permitidos

| Tipo       | Propósito                                              |
| ---------- | ------------------------------------------------------ |
| `feat`     | Nueva funcionalidad                                    |
| `fix`      | Corrección de errores                                  |
| `docs`     | Cambios en la documentación                            |
| `refactor` | Mejoras internas sin cambiar funcionalidad             |
| `test`     | Cambios en pruebas o nuevos tests                      |
| `chore`    | Mantenimiento general (scripts, configs, dependencias) |

### ❌ Errores comunes a evitar

* Mensajes vagos como `update`, `arreglos`, `modificaciones`
* Usar mayúsculas al inicio
* Incluir punto final
* Mezclar muchos cambios en un solo commit

### 📅 Bonus: commit extendido (opcional)

```bash
git commit -m "feat(api): agrega endpoint para registrar sensores" \
            -m "Incluye validación básica del payload y guardado en MongoDB. Aún no se implementan los casos de error."
```

---

## 🌟 Objetivo del ejemplo

Vamos a versionar un nuevo archivo llamado `raspberry-limitaciones.md` ubicado en la carpeta `/docs/`.

---

## 🧹 Paso a paso

### 1. Partimos siempre desde la rama `develop`

```bash
# Nos aseguramos de estar en la rama develop
git checkout develop

# Traemos los últimos cambios del repositorio remoto (por si hubo actualizaciones)
git pull
```

> ✅ `git pull` es un comando que actualiza tu rama local con los últimos cambios del repositorio remoto. Es buena práctica usarlo antes de crear nuevas ramas o comenzar a trabajar.

---

### 2. Creamos una nueva rama de trabajo (feature)

```bash
# Creamos y cambiamos a una nueva rama llamada feature/docs-raspberry
git checkout -b feature/docs-raspberry
```

> 💡 Usamos el prefijo `feature/` seguido de una descripción breve y clara.

---

### 3. Agregamos el nuevo archivo al staging

```bash
# Indicamos a Git que queremos incluir el nuevo archivo en el próximo commit
git add docs/raspberry-limitaciones.md
```

---

### 4. Comiteamos el cambio con convención semántica

```bash
# Guardamos los cambios en el historial de Git con un mensaje claro y semántico
git commit -m "docs(raspberry): agrega limitaciones y optimizaciones"
```

---

### 5. Subimos la rama al repositorio remoto

```bash
# Enviamos la nueva rama al repositorio remoto para compartirla con el equipo
git push origin feature/docs-raspberry
```

---

### 6. Creamos un Pull Request en GitHub/GitLab

* Base: `develop`
* Comparar: `feature/docs-raspberry`
* Agregamos una breve descripción
* Asignamos reviewer si es necesario

---

### 7. Una vez mergeado, limpiamos la rama local y remota

```bash
# Volvemos a develop para dejarla actualizada
git checkout develop

git pull   # Traemos el merge que se hizo desde la plataforma remota

# Borramos la rama local porque ya cumplió su propósito
git branch -d feature/docs-raspberry

# Borramos la rama remota también
git push origin --delete feature/docs-raspberry
```

---

## 🧼 Buenas prácticas recordatorio

* ✅ Usar nombres de ramas descriptivos y consistentes.
* ✅ Hacer commits claros, pequeños y con propósito único.
* ✅ Eliminar ramas que ya no se usen luego del merge.
* ✅ Siempre trabajar sobre `develop` (no sobre `main`).

---

> Este ejemplo sirve de plantilla para cualquier otro cambio, ya sea de código, backend, frontend o documentación. Simple, predecible y limpio.
