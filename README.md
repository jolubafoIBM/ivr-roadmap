# IVR Roadmap Q4 2026 — GitHub Pages

Roadmap interactivo y colaborativo del proyecto IVR Cognitivo Claro.
Todos los cambios se guardan directamente en este repositorio como commits.

---

## 🚀 Configuración inicial (una sola vez)

### Paso 1 — Crear el repositorio en GitHub

1. Ve a [github.com/new](https://github.com/new)
2. **Repository name:** `ivr-roadmap` (o el nombre que prefieras)
3. **Visibility:** Private (recomendado para proyecto cliente)
4. No inicialices con README (lo subimos nosotros)
5. Click **Create repository**

---

### Paso 2 — Subir los archivos

Desde la terminal (o arrastrando en la UI de GitHub):

```bash
# Clona el repo vacío
git clone https://github.com/TU-USUARIO/ivr-roadmap.git
cd ivr-roadmap

# Copia los dos archivos desde tu máquina
# (están en: Backlog Consolidado/roadmap/github-deploy/)
copy "index.html" .
copy "data.json"  .

git add .
git commit -m "feat: initial roadmap Q4 2026"
git push origin main
```

O directamente desde GitHub.com:
1. En el repo → **Add file → Upload files**
2. Arrastra `index.html` y `data.json`
3. Commit message: `feat: initial roadmap Q4 2026`
4. Click **Commit changes**

---

### Paso 3 — Activar GitHub Pages

1. En el repositorio → **Settings** (ícono engranaje)
2. Sección **Pages** (menú izquierdo)
3. **Source:** `Deploy from a branch`
4. **Branch:** `main` → `/root` (raíz)
5. Click **Save**
6. Espera ~1 minuto → aparece la URL:
   ```
   https://TU-USUARIO.github.io/ivr-roadmap/
   ```
7. **Comparte esa URL con el equipo** — eso es todo.

---

### Paso 4 — Crear el Personal Access Token (PAT)

El token permite que el roadmap guarde cambios directamente en GitHub.
**Solo quien va a editar necesita el token.** Quien solo consulta puede abrir la URL sin token.

1. Ve a **GitHub.com → tu avatar → Settings**
2. Menú izquierdo → **Developer settings → Personal access tokens → Tokens (classic)**
3. Click **Generate new token (classic)**
4. **Note:** `ivr-roadmap-editor`
5. **Expiration:** 90 days (o el período que quieras)
6. **Scopes:** marca solo ✅ `repo` (acceso completo al repositorio)
7. Click **Generate token**
8. **COPIA el token ahora** — no lo verás de nuevo. Empieza con `ghp_...`

> ⚠ **El token solo se guarda en tu navegador** (`localStorage`).
> Nunca se sube a GitHub ni sale de tu máquina.

---

### Paso 5 — Configurar el roadmap en el navegador

1. Abre la URL de GitHub Pages
2. En la barra superior aparece el **banner de configuración**:
   - **usuario / organización:** tu usuario de GitHub (ej. `josebarbosa-ibm`)
   - **nombre-del-repo:** `ivr-roadmap`
   - **rama:** `main`
   - **token:** pega tu `ghp_...`
3. Click **Conectar**
4. El roadmap carga los datos desde `data.json` automáticamente

---

## 👥 Uso colaborativo

### Para editar

1. Abre la URL y configura tu token (solo la primera vez en cada navegador)
2. Haz clic en cualquier item → modifica → **Guardar**
3. El botón **💾 Guardar en GitHub** hace un commit con tus cambios
4. Todos los demás ven los cambios en la próxima recarga (auto-refresca cada 2 min)

### Para solo consultar (capacitaciones, reuniones)

1. Abre la URL — **no necesitas token para ver**
2. Click **▶ Presentación** para modo limpio sin botones de edición
3. Click **📊 Capacidad** para mostrar/ocultar las barras de SP por tribu

### Flujo de trabajo recomendado en reuniones

```
Antes de la reunión:
  → Quien lidera abre la URL con su token
  → Activa Modo Presentación para proyectar

Durante la reunión:
  → Sale del modo presentación para editar en vivo
  → Mueve items entre sprints con clic → cambio de sprint target
  → Añade comentarios/decisiones en cada item
  → 💾 Guardar al final de cada bloque de decisiones

Después de la reunión:
  → ⬇ CSV para exportar el acta de decisiones
  → El historial de commits en GitHub guarda qué cambió y cuándo
```

---

## 🔒 Seguridad

| Qué | Dónde está | Quién lo ve |
|---|---|---|
| `index.html` + `data.json` | GitHub (público o privado) | Según visibilidad del repo |
| Token PAT | Solo en tu `localStorage` | Solo tú en ese navegador |
| Historial de cambios | Commits de GitHub | Todo el equipo con acceso al repo |

**Si el repo es privado:** la URL de GitHub Pages también requiere que el visitante tenga acceso al repo, o actives "Public" en Pages settings.

**Alternativa para repo privado visible:** configura el repo como público pero los datos no son sensibles (solo IDs y nombres de historias de usuario).

---

## 🔄 Detección de conflictos

Si dos personas guardan al mismo tiempo:
- La segunda persona verá un **banner de conflicto**
- Puede elegir **Cargar versión remota** (descarta sus cambios locales)
- O **Ignorar y sobrescribir** (sus cambios ganan)

Para evitar conflictos: coordinen quién edita en cada reunión.

---

## 📁 Estructura del repo

```
ivr-roadmap/
├── index.html      ← Aplicación completa (UI + lógica)
├── data.json       ← Datos del roadmap (se actualiza con cada save)
└── README.md       ← Este archivo
```

---

## 🛠 Mantenimiento

### Añadir un nuevo sprint
En el roadmap: click ✏ en el encabezado de cualquier sprint → cambia la etiqueta.
Para añadir Sprint 17+: edita `index.html` — busca el array `SPRINTS` y añade `'s17'`.

### Sincronizar con el CSV del backlog
Exporta con **⬇ CSV** y compáralo con `homologaciones_agrupación.csv`.
El skill `ivr-backlog-sync` puede detectar nuevos items en el Excel y sugerirte añadirlos.

### Resetear a estado inicial
En la barra → **↺ Reset** → recarga desde el `data.json` actual en GitHub.
Para volver al estado original: haz `git revert` en GitHub al commit inicial.
