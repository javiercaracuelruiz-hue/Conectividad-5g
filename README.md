# 5G Fábrica Challenge

Juego tipo Kahoot para la presentación «Conectividad 5G». 10 preguntas basadas en tu PPT y guion.
Los compañeros juegan desde el móvil y tú proyectas la pantalla del presentador con el ranking en directo.

- Jugadores: `https://TU_USUARIO.github.io/juego5g/`
- Presentador (proyector): `https://TU_USUARIO.github.io/juego5g/#host`

## Por qué hace falta Firebase
GitHub Pages solo sirve archivos estáticos: no puede guardar las respuestas de la clase. Por eso usamos
Firebase Realtime Database (gratis, plan Spark, sin tarjeta) como "buzón" compartido.
Sin configurarlo, el juego funciona en **modo demo** (solo entre pestañas del mismo navegador, para probar).

## Paso 1 · Crear la base de datos (5 min)
1. Entra en https://console.firebase.google.com con tu cuenta de Google y pulsa **Crear un proyecto** (puedes desactivar Analytics).
2. Menú **Compilación → Realtime Database → Crear base de datos**. Elige región Bélgica (europe-west1) y **modo de prueba**.
3. Pestaña **Reglas**, pega esto y pulsa **Publicar**:
   ```json
   { "rules": { "game5g": { ".read": true, ".write": true } } }
   ```
4. **Configuración del proyecto (⚙️) → General → Tus apps → icono `</>` (Web)** → registra la app y copia el objeto `firebaseConfig`.
5. Abre `firebase-config.js` y sustituye `window.FIREBASE_CONFIG = null;` por tu configuración:
   ```js
   window.FIREBASE_CONFIG = {
     apiKey: "...", authDomain: "...",
     databaseURL: "https://TU-PROYECTO-default-rtdb.europe-west1.firebasedatabase.app",
     projectId: "...", appId: "..."
   };
   ```
   (La `apiKey` de Firebase web no es secreta; la seguridad la dan las reglas.)

## Paso 2 · Publicar en GitHub Pages
1. En GitHub: **New repository** → nombre `juego5g`, público.
2. Sube `index.html` y `firebase-config.js` (y este README si quieres).
3. **Settings → Pages → Deploy from a branch → main / (root) → Save**.
4. En 1-2 minutos estará en `https://TU_USUARIO.github.io/juego5g/`.

## Cómo usarlo en clase
1. Antes de exponer, abre `…/#host` en el ordenador conectado al proyector.
2. Al llegar a la diapositiva 10 (o tras la 9), muestra el QR/enlace: los compañeros entran y ponen su nombre.
3. Pulsa **Empezar**. Cada pregunta dura 20 s; se muestra el resultado solo cuando todos responden o se acaba el tiempo (o con el botón).
4. Puntos: 500 por acertar + hasta 500 extra por rapidez.
5. Al final verás el podio, la clasificación y el % de aciertos por pregunta.
6. **Reiniciar juego** (abajo del todo) borra los datos para otra ronda.

Duración aproximada: 6-8 minutos con 25-30 personas.

## Personalizar
Las preguntas están al inicio de `index.html` (`QUESTIONS`). Cambia el texto, las opciones, `a` (índice de la correcta, empezando en 0) y `e` (explicación). `LIMIT` son los segundos por pregunta.

## Probar en local
`python3 -m http.server 8000` dentro de la carpeta y abre `http://localhost:8000/#host` y, en otras pestañas, `http://localhost:8000/`.
