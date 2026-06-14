# ¿Cuál es tu ministerio? · Test JACM

Aplicación web tipo test de personalidad ("¿qué casa eres?") que ayuda a los
jóvenes a descubrir en qué **ministerio** de los Jóvenes de Acción Católica
Mercedaria (JACM) encaja mejor su forma de servir.

Pensada como herramienta de **acogida y promoción**: alguien que llega al grupo
responde unas preguntas y recibe una orientación cálida sobre dónde podría servir,
con una invitación a conversarlo con la coordinación.

> Parroquia San Ramón Nonato · Maracaibo, Zulia · *"Libres para liberar"*

---

## Características

- 12 preguntas de personalidad orientadas a 5 ministerios.
- Resultado con ministerio principal + un "también encajarías en…".
- Diseño basado en la identidad visual del grupo (vino, dorado, escudo).
- Barra de progreso temática (cadena que se libera eslabón a eslabón).
- Música de fondo opcional con botón de play/pausa.
- Fotos personalizables: del grupo en el inicio y de cada ministerio en el resultado.
- Progreso guardado en `localStorage` (retoma un test a medias).
- Botón de compartir (usa el menú nativo en móvil; copia el enlace en escritorio).
- Responsive y móvil-first. Respeta `prefers-reduced-motion`.

---

## Los 5 ministerios

| Ministerio | Perfil que encaja | Coordina |
|---|---|---|
| **Promoción** | Comunicador, creativo, acoge a quien llega | Andrea Leal |
| **Formación** | Estudioso, didáctico, le gusta enseñar | Hans Meyer |
| **Liturgia** | Contemplativo, detallista, reverente | María Simoes |
| **Música** | Sensible, expresivo, constante con el ensayo | Ángel Atencio |
| **Finanzas** | Organizado, íntegro, planificador | Gabriela Ferrer |

El rol de Secretario no es un resultado del test: lo designa la coordinación.

---

## Cómo usarlo

Es un solo archivo HTML, sin dependencias ni build. Para verlo localmente, abre
`test_ministerios_jacm.html` en cualquier navegador.

> **Nota:** la música y el guardado de progreso (`localStorage`) requieren abrir
> el archivo desde un navegador real o un servidor; no funcionan dentro de algunos
> visores embebidos (sandbox).

Para servirlo localmente con un servidor simple:

```bash
# Python 3
python -m http.server 8000
# luego abre http://localhost:8000/test_ministerios_jacm.html
```

---

## Configuración

Toda la personalización se hace en el bloque `CONFIG`, al inicio del archivo.
Deja una cadena vacía `""` para mostrar el placeholder en su lugar.

```js
const CONFIG = {
  // Audio de fondo (.mp3/.ogg). "" oculta el botón de música.
  audio: "",

  // Logo de Acción Católica (inicio). "" usa el escudo dibujado por defecto.
  logoAC: "https://raw.githubusercontent.com/VKneider/jac-birthday-card/master/logo%20ac.png",

  // 3 fotos del grupo para el inicio (cuadradas se ven mejor).
  fotosInicio: ["", "", ""],

  // 1 foto por ministerio para la pantalla de resultado.
  fotosMinisterio: {
    promocion: "",
    formacion: "",
    liturgia:  "",
    musica:    "",
    finanzas:  ""
  }
};
```

**Sobre las imágenes:** usa URLs públicas (por ejemplo, archivos del propio repo
servidos vía `raw.githubusercontent.com`, o imágenes en el hosting). Si una imagen
no carga, la app muestra un respaldo automáticamente.

**Sobre la música:** los navegadores no permiten reproducir audio automáticamente
sin una interacción del usuario. Por eso la música intenta arrancar al pulsar
"Empezar", y el botón de la esquina superior derecha permite pausar y reanudar.

---

## Editar las preguntas

Las preguntas están en el arreglo `QUESTIONS`. Cada pregunta tiene un texto `q` y
una lista de opciones `opts`. Cada opción suma puntos a uno o dos ministerios
mediante `s`:

```js
{ q: "Tu pregunta aquí", opts: [
  { t: "Texto de la opción", s: { p: 2 } },        // +2 a Promoción
  { t: "Otra opción",        s: { l: 1, n: 1 } },  // +1 Liturgia, +1 Finanzas
]}
```

Claves de puntuación: `p` Promoción · `f` Formación · `l` Liturgia · `m` Música ·
`n` Finanzas. Al terminar, gana el ministerio con más puntos.

---

## Despliegue

Al ser un sitio estático, se publica en cualquier hosting gratuito.

**GitHub Pages**

1. Sube el archivo al repositorio.
2. En *Settings → Pages*, elige la rama (`master`/`main`) y la carpeta raíz.
3. El test quedará disponible en `https://<usuario>.github.io/<repo>/test_ministerios_jacm.html`.

También funciona en Vercel, Netlify o cualquier servidor estático arrastrando el
archivo.

---

## Estructura del proyecto

```
.
├── test_ministerios_jacm.html   # La aplicación completa (HTML + CSS + JS)
├── ministerios_jacm.md          # Fuente de contenido: perfiles y ejes del test
├── logo ac.png                  # Logo de Acción Católica
└── README.md
```

---

## Tecnología

HTML, CSS y JavaScript puro. Sin frameworks, sin dependencias, sin build.
Tipografías: Fraunces y Nunito Sans (Google Fonts).

---

## Créditos

Desarrollado para los **Jóvenes de Acción Católica Mercedaria**, Parroquia San
Ramón Nonato, Maracaibo.

*"Viva Cristo Rey y su amor sea nuestra ley" — "Libres para liberar"*
