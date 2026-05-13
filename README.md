# ⚔ Aincrad Online — Floor 1

Un MMO de navegador estilo Sword Art Online con combate en tiempo real, sistema de clases, inventario, chat y comercio entre jugadores.

---

## 🚀 Cómo publicarlo en GitHub Pages

### Paso 1 — Subir a GitHub

1. Creá un repositorio nuevo en [github.com](https://github.com) (ej: `aincrad-online`)
2. Subí estos archivos al repositorio:
   - `index.html`
   - `README.md`
3. En tu repositorio, andá a **Settings → Pages**
4. En *Source*, seleccioná **Deploy from a branch → main → / (root)**
5. Guardá. En unos segundos el juego estará en:
   ```
   https://TU_USUARIO.github.io/aincrad-online/
   ```

---

## 🔥 Configurar Firebase (para multijugador real)

Sin Firebase el juego funciona en **modo demo local** (un solo jugador, datos en `localStorage`).

Para activar el multijugador real necesitás un proyecto Firebase **gratuito**:

### 1. Crear el proyecto

1. Andá a [console.firebase.google.com](https://console.firebase.google.com)
2. Hacé clic en **Agregar proyecto** → ponele un nombre (ej: `aincrad-online`)
3. Desactivá Google Analytics si querés (no es necesario) → **Crear proyecto**

### 2. Activar Authentication

1. En el menú izquierdo: **Authentication → Comenzar**
2. Pestaña **Métodos de acceso → Email/Contraseña → Habilitar → Guardar**

### 3. Activar Realtime Database

1. En el menú izquierdo: **Realtime Database → Crear base de datos**
2. Elegí una región (ej: `us-central1`) → **Siguiente**
3. Seleccioná **Modo de prueba** → **Habilitar**
4. Luego en la pestaña **Reglas**, reemplazá el contenido con:

```json
{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null",
    "chat": {
      ".read": "auth != null",
      ".write": "auth != null"
    }
  }
}
```

5. Publicá las reglas.

### 4. Obtener las credenciales

1. En **Configuración del proyecto** (engranaje ⚙ arriba a la izquierda) → **General**
2. Bajá hasta **Tus apps** → clic en `</>` (Web)
3. Registrá la app con un nombre → **Registrar**
4. Copiá el objeto `firebaseConfig` que aparece

### 5. Pegar las credenciales en el juego

Abrí `index.html` y buscá esta sección al principio del primer `<script>`:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyDEMO_REPLACE_WITH_YOUR_KEY",
  authDomain: "aincrad-online.firebaseapp.com",
  ...
};
```

Reemplazala con tus propias credenciales. Guardá y volvé a subir `index.html` a GitHub.

### 6. Agregar GitHub Pages como dominio autorizado

1. En Firebase: **Authentication → Settings → Dominios autorizados**
2. Hacé clic en **Agregar dominio**
3. Ingresá: `TU_USUARIO.github.io`

---

## 🎮 Controles

| Tecla | Acción |
|-------|--------|
| `WASD` / `↑↓←→` | Mover personaje |
| `Click` | Atacar al monstruo más cercano |
| `2` | Usar poción de HP |
| `3` | Usar poción de MP |
| `E` | Abrir cofre cercano |
| `I` | Abrir/cerrar inventario |
| `Tab` | Ver/ocultar equipo |

---

## 🧙 Clases disponibles

| Clase | Fortaleza |
|-------|-----------|
| Sword | Alto ATK, DEF media — clase balanceada |
| Mage | Magia AoE, alto MP |
| Archer | Largo alcance, alta velocidad |
| Shield | Tank, altísima DEF |
| Assassin | Críticos devastadores, ultra velocidad |
| Healer | Soporte y curación |

---

## ⚠ Permadeath

Este juego implementa **muerte permanente**. Si tu HP llega a 0, el personaje se elimina definitivamente de Firebase. ¡Sobreviví!

---

## 📁 Estructura del proyecto

```
aincrad-online/
├── index.html    ← Todo el juego (HTML + CSS + JS en un solo archivo)
└── README.md     ← Esta guía
```

No se necesita servidor, npm, ni compilación. Es HTML puro.
