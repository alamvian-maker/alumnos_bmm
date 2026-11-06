# alumnos_bmm
Aquí encuentras tus tareas, guías, clases en video y avisos del curso. Revísala constantemente
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Portal del curso · Ciencia, Tecnología y Pensamiento Matemático</title>
<meta name="description" content="Portal de avisos, tareas, videos y encuestas para estudiantes.">

<!-- ======================================================================
     PORTAL PARA ESTUDIANTES — UN SOLO ARCHIVO
     ----------------------------------------------------------------------
     CÓMO EDITARLO (sin saber programar):
       1. Busca el bloque que dice "CONFIGURACIÓN DEL CURSO" al final del
          archivo (dentro de <script>). Ahí están TODOS los textos, tareas,
          videos, fechas y avisos que normalmente vas a cambiar.
       2. Cambia únicamente lo que está entre comillas "así".
       3. Guarda el archivo y ábrelo en el navegador para ver los cambios.
     Los textos fijos (títulos de sección, etiquetas de formularios) están
     en el HTML de abajo; también puedes cambiarlos buscándolos.
     ====================================================================== -->

<style>
  /* ---------- COLORES Y MEDIDAS (cámbialos aquí si quieres otra paleta) ---------- */
  :root {
    --color-principal: #2b59c3;      /* azul de botones y encabezado */
    --color-principal-osc: #1d3f8f;
    --color-acento: #f59e0b;         /* ámbar para resaltar */
    --fondo: #f3f6fb;
    --tarjeta: #ffffff;
    --texto: #1f2937;
    --texto-suave: #4b5563;
    --borde: #d9e0ec;
    --verde: #15803d;  --verde-fondo: #dcfce7;
    --rojo: #b91c1c;   --rojo-fondo: #fee2e2;
    --azul: #1d4ed8;   --azul-fondo: #dbeafe;
    --gris: #374151;   --gris-fondo: #e5e7eb;
    --radio: 16px;
    --sombra: 0 2px 10px rgba(31, 41, 55, .08);
  }

  /* ---------- BASE ---------- */
  * { box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body {
    margin: 0;
    font-family: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    font-size: 1.05rem;
    line-height: 1.6;
    color: var(--texto);
    background: var(--fondo);
  }
  h1, h2, h3 { line-height: 1.25; margin: 0 0 .5rem; }
  h2 { font-size: 1.5rem; }
  h3 { font-size: 1.1rem; }
  p  { margin: 0 0 .75rem; }
  a  { color: var(--color-principal); }
  .contenedor { width: min(1100px, 100% - 2rem); margin-inline: auto; }

  /* Enlace "saltar al contenido" para lectores de pantalla y teclado */
  .saltar {
    position: absolute; left: -999px; top: 0;
    background: #000; color: #fff; padding: .6rem 1rem; z-index: 100;
  }
  .saltar:focus { left: 0; }

  /* Foco visible para navegar con teclado */
  :focus-visible { outline: 3px solid var(--color-acento); outline-offset: 2px; }

  /* ---------- ENCABEZADO ---------- */
  header.portada {
    background: linear-gradient(135deg, var(--color-principal), var(--color-principal-osc));
    color: #fff;
    padding: 2.5rem 0 3.5rem;
  }
  .portada .etiqueta {
    display: inline-block; background: rgba(255,255,255,.18);
    padding: .2rem .8rem; border-radius: 999px; font-size: .9rem; margin-bottom: .75rem;
  }
  .portada h1 { font-size: clamp(1.7rem, 5vw, 2.6rem); margin-bottom: .4rem; }
  .portada .subtitulo { opacity: .92; margin: 0; }

  /* Menú de navegación */
  nav.menu { background: var(--tarjeta); box-shadow: var(--sombra); position: sticky; top: 0; z-index: 50; }
  nav.menu ul {
    list-style: none; margin: 0; padding: .4rem 0; display: flex; gap: .25rem;
    overflow-x: auto; -webkit-overflow-scrolling: touch;
  }
  nav.menu a {
    display: block; white-space: nowrap; padding: .55rem .9rem; border-radius: 10px;
    text-decoration: none; color: var(--texto); font-weight: 600; font-size: .95rem;
  }
  nav.menu a:hover { background: var(--azul-fondo); color: var(--azul); }

  /* ---------- AVISOS (dentro del encabezado, sobresalen sobre el fondo) ---------- */
  .avisos {
    margin-top: -2rem;
    background: var(--tarjeta); border-radius: var(--radio); box-shadow: var(--sombra);
    padding: 1.25rem 1.5rem; border-left: 6px solid var(--color-acento);
  }
  .avisos ul { margin: .25rem 0 0; padding-left: 1.2rem; }
  .avisos li { margin-bottom: .35rem; }

  /* ---------- SECCIONES Y TARJETAS ---------- */
  main { padding-bottom: 2rem; }
  section { padding-top: 2.5rem; scroll-margin-top: 4rem; }
  .intro-seccion { color: var(--texto-suave); margin-bottom: 1.25rem; }
  .rejilla { display: grid; gap: 1rem; grid-template-columns: repeat(auto-fill, minmax(290px, 1fr)); }
  .tarjeta {
    background: var(--tarjeta); border: 1px solid var(--borde); border-radius: var(--radio);
    padding: 1.15rem 1.25rem; box-shadow: var(--sombra);
    display: flex; flex-direction: column;
  }

  /* ---------- TAREAS ---------- */
  .filtros { display: flex; flex-wrap: wrap; gap: .5rem; margin-bottom: 1rem; }
  .filtro {
    border: 1px solid var(--borde); background: var(--tarjeta); color: var(--texto);
    padding: .45rem 1rem; border-radius: 999px; cursor: pointer; font: inherit; font-size: .95rem;
  }
  .filtro[aria-pressed="true"] { background: var(--color-principal); color: #fff; border-color: var(--color-principal); }

  .tarea .cabecera { display: flex; justify-content: space-between; gap: .75rem; align-items: flex-start; }
  .insignia {
    flex-shrink: 0; font-size: .8rem; font-weight: 700; padding: .2rem .7rem; border-radius: 999px;
    text-transform: uppercase; letter-spacing: .03em;
  }
  .insignia.nueva    { background: var(--azul-fondo);  color: var(--azul); }
  .insignia.urgente  { background: var(--rojo-fondo);  color: var(--rojo); }
  .insignia.entregada{ background: var(--verde-fondo); color: var(--verde); }
  .insignia.pendiente{ background: var(--gris-fondo);  color: var(--gris); }
  .tarea.urgente  { border-top: 5px solid var(--rojo); }
  .tarea.nueva    { border-top: 5px solid var(--azul); }
  .tarea.entregada{ border-top: 5px solid var(--verde); }
  .tarea.pendiente{ border-top: 5px solid #9ca3af; }
  .tarea .fecha { font-weight: 600; color: var(--texto-suave); margin-bottom: .5rem; }
  .tarea .descripcion { flex: 1; }
  .materiales { display: flex; flex-wrap: wrap; gap: .5rem; margin-top: .5rem; }

  /* ---------- BOTONES ---------- */
  .boton {
    display: inline-flex; align-items: center; gap: .4rem; justify-content: center;
    background: var(--color-principal); color: #fff; border: 0; border-radius: 12px;
    padding: .65rem 1.2rem; font: inherit; font-weight: 600; cursor: pointer; text-decoration: none;
  }
  .boton:hover { background: var(--color-principal-osc); }
  .boton.secundario { background: var(--azul-fondo); color: var(--azul); }
  .boton.secundario:hover { background: #bfdbfe; }
  .boton[disabled] { opacity: .6; cursor: wait; }

  /* ---------- VIDEOS ---------- */
  .video-marco {
    position: relative; width: 100%; aspect-ratio: 16 / 9; background: #0f172a;
    border-radius: 12px; overflow: hidden; margin-bottom: .75rem;
  }
  .video-marco iframe { position: absolute; inset: 0; width: 100%; height: 100%; border: 0; }
  .video-vacio {
    position: absolute; inset: 0; display: grid; place-items: center; text-align: center;
    color: #cbd5e1; padding: 1rem; font-size: .95rem;
  }

  /* ---------- FORMULARIOS ---------- */
  .formulario { max-width: 720px; }
  fieldset { border: 1px solid var(--borde); border-radius: 12px; margin: 0 0 1.1rem; padding: .8rem 1rem 1rem; }
  legend { font-weight: 700; padding: 0 .4rem; }
  label { display: block; font-weight: 600; margin-bottom: .3rem; }
  .opcion { display: flex; align-items: center; gap: .6rem; padding: .35rem 0; font-weight: 400; }
  .opcion input { width: 1.2rem; height: 1.2rem; accent-color: var(--color-principal); }
  input[type="text"], select, textarea {
    width: 100%; font: inherit; padding: .65rem .8rem; border: 1px solid #9ca3af;
    border-radius: 10px; background: #fff; color: var(--texto);
  }
  textarea { min-height: 150px; resize: vertical; }
  .campo { margin-bottom: 1.1rem; }
  .ayuda { font-size: .9rem; color: var(--texto-suave); margin-top: .25rem; }
  .escala { display: flex; flex-wrap: wrap; gap: .5rem; }
  .escala .opcion {
    border: 1px solid var(--borde); border-radius: 10px; padding: .5rem .8rem; background: #fff;
  }

  /* Mensajes de confirmación */
  .mensaje { margin-top: 1rem; padding: .9rem 1.1rem; border-radius: 12px; display: none; font-weight: 600; }
  .mensaje.visible { display: block; }
  .mensaje.ok    { background: var(--verde-fondo); color: #14532d; }
  .mensaje.error { background: var(--rojo-fondo);  color: #7f1d1d; }

  /* ---------- PIE DE PÁGINA ---------- */
  footer { background: #111827; color: #e5e7eb; margin-top: 3rem; padding: 2.5rem 0; }
  footer h2 { color: #fff; font-size: 1.25rem; }
  footer .columnas { display: grid; gap: 1.5rem; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); }
  footer ul { margin: 0; padding-left: 1.1rem; }
  footer li { margin-bottom: .4rem; }
  footer .pie-final { margin-top: 1.5rem; font-size: .9rem; color: #9ca3af; border-top: 1px solid #374151; padding-top: 1rem; }

  /* ---------- AJUSTES PARA TELÉFONO ---------- */
  @media (max-width: 600px) {
    body { font-size: 1rem; }
    .avisos { padding: 1rem; }
    .boton { width: 100%; }
    .materiales .boton { width: auto; flex: 1 1 100%; }
  }
  /* Respeta a quien prefiere menos movimiento */
  @media (prefers-reduced-motion: reduce) { html { scroll-behavior: auto; } }
</style>
</head>

<body>
<a class="saltar" href="#contenido">Saltar al contenido</a>

<!-- ============================ 1. ENCABEZADO ============================ -->
<header class="portada">
  <div class="contenedor">
    <span class="etiqueta" id="grupo"></span>
    <h1 id="titulo-curso"></h1>
    <p class="subtitulo" id="subtitulo-curso"></p>
  </div>
</header>

<nav class="menu" aria-label="Navegación principal">
  <div class="contenedor">
    <ul>
      <li><a href="#tareas">Tareas</a></li>
      <li><a href="#videos">Videos</a></li>
      <li><a href="#encuesta">Encuesta</a></li>
      <li><a href="#buzon">Dudas y sugerencias</a></li>
      <li><a href="#fechas">Fechas clave</a></li>
    </ul>
  </div>
</nav>

<main id="contenido">
  <div class="contenedor">

    <!-- Bienvenida y avisos (se llenan desde la configuración) -->
    <div class="avisos" role="region" aria-labelledby="avisos-titulo">
      <h2 id="avisos-titulo">👋 <span id="bienvenida-titulo"></span></h2>
      <p id="bienvenida-texto"></p>
      <ul id="lista-avisos"></ul>
    </div>

    <!-- ===================== 2. TAREAS Y MATERIALES ===================== -->
    <section id="tareas" aria-labelledby="tareas-titulo">
      <h2 id="tareas-titulo">📚 Tareas y materiales</h2>
      <p class="intro-seccion">Revisa la fecha límite de cada actividad y descarga las guías que necesites.</p>

      <div class="filtros" role="group" aria-label="Filtrar tareas por estado">
        <button class="filtro" data-filtro="todas" aria-pressed="true">Todas</button>
        <button class="filtro" data-filtro="urgente" aria-pressed="false">Urgentes</button>
        <button class="filtro" data-filtro="nueva" aria-pressed="false">Nuevas</button>
        <button class="filtro" data-filtro="pendiente" aria-pressed="false">Pendientes</button>
        <button class="filtro" data-filtro="entregada" aria-pressed="false">Entregadas</button>
      </div>

      <div class="rejilla" id="lista-tareas" aria-live="polite"></div>
    </section>

    <!-- ======================= 3. VIDEOS ======================= -->
    <section id="videos" aria-labelledby="videos-titulo">
      <h2 id="videos-titulo">🎬 Recursos en video</h2>
      <p class="intro-seccion">Clases grabadas y explicaciones. Puedes verlas las veces que necesites.</p>
      <div class="rejilla" id="lista-videos"></div>
    </section>

    <!-- ================== 4. ENCUESTA E INTERACCIÓN ================== -->
    <section id="encuesta" aria-labelledby="encuesta-titulo">
      <h2 id="encuesta-titulo">📝 Encuesta rápida</h2>
      <p class="intro-seccion" id="encuesta-intro">Tu opinión me ayuda a organizar mejor las clases. Toma menos de un minuto.</p>

      <form class="tarjeta formulario" id="form-encuesta" novalidate>
        <!-- Pregunta 1: escala de comprensión (puedes cambiar el texto de la pregunta) -->
        <fieldset>
          <legend>1. ¿Qué tan bien comprendiste el último tema?</legend>
          <div class="escala">
            <label class="opcion"><input type="radio" name="comprension" value="1" required> 1 · Nada</label>
            <label class="opcion"><input type="radio" name="comprension" value="2"> 2 · Poco</label>
            <label class="opcion"><input type="radio" name="comprension" value="3"> 3 · Regular</label>
            <label class="opcion"><input type="radio" name="comprension" value="4"> 4 · Bien</label>
            <label class="opcion"><input type="radio" name="comprension" value="5"> 5 · Muy bien</label>
          </div>
        </fieldset>

        <!-- Pregunta 2: horario de asesoría (edita las opciones) -->
        <div class="campo">
          <label for="horario">2. ¿Qué horario prefieres para asesorías?</label>
          <select id="horario" name="horario" required>
            <option value="">Selecciona una opción…</option>
            <option>Lunes por la tarde</option>
            <option>Miércoles por la tarde</option>
            <option>Viernes por la tarde</option>
            <option>Sábado por la mañana</option>
          </select>
        </div>

        <!-- Pregunta 3: votación de temas (edita las opciones) -->
        <fieldset>
          <legend>3. ¿Qué temas quieres repasar? (puedes elegir varios)</legend>
          <label class="opcion"><input type="checkbox" name="temas" value="Tema 1"> Tema 1</label>
          <label class="opcion"><input type="checkbox" name="temas" value="Tema 2"> Tema 2</label>
          <label class="opcion"><input type="checkbox" name="temas" value="Tema 3"> Tema 3</label>
        </fieldset>

        <button class="boton" type="submit">Enviar respuestas</button>
        <div class="mensaje" id="msg-encuesta" role="status" aria-live="polite"></div>
      </form>
    </section>

    <!-- =================== 5. DUDAS Y SUGERENCIAS =================== -->
    <section id="buzon" aria-labelledby="buzon-titulo">
      <h2 id="buzon-titulo">💬 Buzón de dudas y sugerencias</h2>
      <p class="intro-seccion">Escribe tu duda sobre una tarea o una sugerencia. Puedes dejar tu nombre o enviarlo de forma anónima.</p>

      <form class="tarjeta formulario" id="form-buzon" novalidate>
        <div class="campo">
          <label for="nombre">Nombre (opcional)</label>
          <input type="text" id="nombre" name="nombre" autocomplete="name" placeholder="Déjalo vacío si prefieres ser anónimo">
        </div>

        <div class="campo">
          <label for="tipo">Tipo de mensaje</label>
          <select id="tipo" name="tipo">
            <option>Duda sobre una tarea</option>
            <option>Duda sobre un tema</option>
            <option>Sugerencia</option>
            <option>Otro</option>
          </select>
        </div>

        <div class="campo">
          <label for="mensaje">Tu mensaje</label>
          <textarea id="mensaje" name="mensaje" maxlength="1000" required aria-describedby="contador"></textarea>
          <div class="ayuda" id="contador">0 / 1000 caracteres</div>
        </div>

        <button class="boton" type="submit">Enviar mensaje</button>
        <div class="mensaje" id="msg-buzon" role="status" aria-live="polite"></div>
      </form>
    </section>

  </div>
</main>

<!-- ========================= 6. PIE DE PÁGINA ========================= -->
<footer>
  <div class="contenedor">
    <div class="columnas">
      <div id="fechas">
        <h2>📅 Fechas clave del periodo</h2>
        <ul id="lista-fechas"></ul>
      </div>
      <div>
        <h2>🔄 Actualización de la plataforma</h2>
        <p id="texto-actualizacion"></p>
        <ul id="lista-recordatorios"></ul>
      </div>
    </div>
    <p class="pie-final" id="pie-final"></p>
  </div>
</footer>


<script>
/* =========================================================================
   CONFIGURACIÓN DEL CURSO  ← EDITA SOLO ESTA PARTE
   -------------------------------------------------------------------------
   Reglas sencillas:
   • Cambia solo el texto que está entre comillas "así".
   • Para agregar una tarea/video/aviso: copia un bloque completo { ... },
     pégalo debajo (con una coma al final) y cambia sus textos.
   • Para quitar uno: borra el bloque completo { ... } con su coma.
   • Las fechas se escriben así: "2026-11-20"  (año-mes-día).
   ========================================================================= */
const CONFIG = {

  /* ----- ENCABEZADO ----- */
  grupo: "Bachillerato Nacional Margarita Maza · Sede Calderón",
  titulo: "Ciencia, Tecnología y Pensamiento Matemático",
  subtitulo: "Portal de avisos, tareas y recursos para estudiantes",

  /* ----- BIENVENIDA Y AVISOS ----- */
  bienvenida: {
    titulo: "¡Bienvenidas y bienvenidos!",
    texto: "En esta página encontrarás todo lo que necesitas para el curso: tareas, materiales, videos y un espacio para tus dudas. Revísala al menos dos veces por semana.",
    avisos: [
      "📌 Aviso 1: escribe aquí una noticia importante.",
      "📌 Aviso 2: por ejemplo, un cambio de fecha o de horario.",
      "📌 Aviso 3: un recordatorio general para el grupo."
    ]
  },

  /* ----- TAREAS -----
     estado: "nueva" | "urgente" | "pendiente" | "entregada"
     materiales: lista de archivos para descargar. En "enlace" pon la ruta o
                 URL del PDF/Word (por ejemplo "materiales/guia1.pdf" si el
                 archivo está en una carpeta junto a esta página, o un enlace
                 de Google Drive). Si no hay material, deja: materiales: []   */
  tareas: [
    {
      titulo: "Tarea 1: Título de la actividad",
      estado: "urgente",
      fecha: "2026-11-12",
      descripcion: "Describe con claridad qué deben hacer: qué entregar, en qué formato y por qué medio.",
      materiales: [
        { nombre: "Guía (PDF)",  enlace: "materiales/guia-1.pdf" },
        { nombre: "Formato (Word)", enlace: "materiales/formato-1.docx" }
      ]
    },
    {
      titulo: "Tarea 2: Título de la actividad",
      estado: "nueva",
      fecha: "2026-11-19",
      descripcion: "Instrucciones breves y claras de la segunda actividad.",
      materiales: [
        { nombre: "Guía (PDF)", enlace: "materiales/guia-2.pdf" }
      ]
    },
    {
      titulo: "Tarea 3: Título de la actividad",
      estado: "pendiente",
      fecha: "2026-11-26",
      descripcion: "Actividad próxima. Más adelante agregarás aquí el material.",
      materiales: []
    },
    {
      titulo: "Tarea 0: Actividad ya entregada",
      estado: "entregada",
      fecha: "2026-10-30",
      descripcion: "Ejemplo de una actividad cerrada. Se conserva como consulta.",
      materiales: [
        { nombre: "Material (PDF)", enlace: "materiales/guia-0.pdf" }
      ]
    }
  ],

  /* ----- VIDEOS -----
     embed: enlace de INCRUSTACIÓN del video.
       • YouTube: "https://www.youtube-nocookie.com/embed/ID_DEL_VIDEO"
         (el ID es lo que va después de "v=" en el enlace normal del video;
          en youtube.com/watch?v=ABC123 el ID es ABC123)
       • Vimeo:   "https://player.vimeo.com/video/NUMERO_DEL_VIDEO"
     Si lo dejas vacío "", se muestra un recuadro con el aviso "Próximamente". */
  videos: [
    {
      titulo: "Clase 1: Título del tema",
      descripcion: "Explicación del tema de la semana. Duración aproximada: 15 minutos.",
      embed: ""
    },
    {
      titulo: "Clase 2: Título del tema",
      descripcion: "Ejercicios resueltos paso a paso.",
      embed: ""
    }
  ],

  /* ----- FECHAS CLAVE (pie de página) ----- */
  fechas: [
    "Inicio del periodo: escribe la fecha",
    "Primera evaluación parcial: escribe la fecha",
    "Entrega de proyecto final: escribe la fecha",
    "Cierre de calificaciones: escribe la fecha"
  ],

  /* ----- ACTUALIZACIÓN DE LA PLATAFORMA (pie de página) ----- */
  actualizacion: "Esta página se actualiza los lunes y jueves por la tarde.",
  recordatorios: [
    "Revisa siempre la fecha límite de cada tarea.",
    "Las dudas del buzón se responden en clase o en el siguiente aviso.",
    "Entrega tus actividades por el medio indicado en cada tarea."
  ],
  pieFinal: "Docente: escribe tu nombre · Contacto institucional: escribe el medio autorizado",

  /* ----- ENVÍO DE FORMULARIOS (opcional, ver explicación) -----
     Una página HTML sola NO puede guardar respuestas. Mientras este campo
     esté vacío "", los formularios solo SIMULAN el envío (el alumno ve el
     mensaje de agradecimiento, pero tú no recibes nada).
     Para recibir respuestas de verdad:
       1) Crea un formulario gratuito en https://formspree.io (o similar)
       2) Pega aquí su dirección, por ejemplo: "https://formspree.io/f/xxxxxxx"
     Las respuestas te llegarán por correo.                                  */
  endpointEncuesta: "",
  endpointBuzon: ""
};


/* =========================================================================
   FIN DE LA CONFIGURACIÓN — de aquí hacia abajo no necesitas cambiar nada
   ========================================================================= */

/* Pequeña ayuda: busca un elemento por su id */
const $ = (id) => document.getElementById(id);

/* Convierte "2026-11-12" en "jueves 12 de noviembre de 2026" */
function formatearFecha(iso) {
  const [a, m, d] = iso.split("-").map(Number);
  const fecha = new Date(a, m - 1, d);
  return fecha.toLocaleDateString("es-MX", { weekday: "long", day: "numeric", month: "long", year: "numeric" });
}

/* Texto de cada estado */
const ETIQUETAS = { nueva: "Nueva", urgente: "Urgente", pendiente: "Pendiente", entregada: "Entregada" };

/* Crea un elemento con texto seguro (evita problemas con caracteres especiales) */
function el(etiqueta, clase, texto) {
  const e = document.createElement(etiqueta);
  if (clase) e.className = clase;
  if (texto !== undefined) e.textContent = texto;
  return e;
}

/* ---------- Encabezado, avisos y pie ---------- */
function pintarTextosGenerales() {
  document.title = "Portal del curso · " + CONFIG.titulo;
  $("grupo").textContent = CONFIG.grupo;
  $("titulo-curso").textContent = CONFIG.titulo;
  $("subtitulo-curso").textContent = CONFIG.subtitulo;
  $("bienvenida-titulo").textContent = CONFIG.bienvenida.titulo;
  $("bienvenida-texto").textContent = CONFIG.bienvenida.texto;
  CONFIG.bienvenida.avisos.forEach(t => $("lista-avisos").appendChild(el("li", "", t)));
  CONFIG.fechas.forEach(t => $("lista-fechas").appendChild(el("li", "", t)));
  CONFIG.recordatorios.forEach(t => $("lista-recordatorios").appendChild(el("li", "", t)));
  $("texto-actualizacion").textContent = CONFIG.actualizacion;
  $("pie-final").textContent = CONFIG.pieFinal;
}

/* ---------- Tareas ---------- */
function pintarTareas(filtro) {
  const cont = $("lista-tareas");
  cont.innerHTML = "";
  const tareas = CONFIG.tareas.filter(t => filtro === "todas" || t.estado === filtro);

  if (tareas.length === 0) {
    cont.appendChild(el("p", "intro-seccion", "No hay tareas con este estado."));
    return;
  }

  tareas.forEach(t => {
    const tarjeta = el("article", "tarjeta tarea " + t.estado);

    const cab = el("div", "cabecera");
    cab.appendChild(el("h3", "", t.titulo));
    cab.appendChild(el("span", "insignia " + t.estado, ETIQUETAS[t.estado] || t.estado));
    tarjeta.appendChild(cab);

    tarjeta.appendChild(el("p", "fecha", "📅 Fecha límite: " + formatearFecha(t.fecha)));
    tarjeta.appendChild(el("p", "descripcion", t.descripcion));

    if (t.materiales && t.materiales.length) {
      const caja = el("div", "materiales");
      t.materiales.forEach(m => {
        const a = el("a", "boton secundario", "⬇ " + m.nombre);
        a.href = m.enlace;
        a.setAttribute("download", "");
        a.target = "_blank";
        a.rel = "noopener";
        caja.appendChild(a);
      });
      tarjeta.appendChild(caja);
    }
    cont.appendChild(tarjeta);
  });
}

/* Botones de filtro */
document.querySelectorAll(".filtro").forEach(btn => {
  btn.addEventListener("click", () => {
    document.querySelectorAll(".filtro").forEach(b => b.setAttribute("aria-pressed", "false"));
    btn.setAttribute("aria-pressed", "true");
    pintarTareas(btn.dataset.filtro);
  });
});

/* ---------- Videos ---------- */
function pintarVideos() {
  const cont = $("lista-videos");
  CONFIG.videos.forEach(v => {
    const tarjeta = el("article", "tarjeta");
    const marco = el("div", "video-marco");

    if (v.embed) {
      const iframe = document.createElement("iframe");
      iframe.src = v.embed;
      iframe.title = "Video: " + v.titulo;
      iframe.loading = "lazy";
      iframe.allow = "accelerometer; encrypted-media; gyroscope; picture-in-picture; fullscreen";
      iframe.allowFullscreen = true;
      marco.appendChild(iframe);
    } else {
      marco.appendChild(el("div", "video-vacio", "🎥 Video próximamente"));
    }

    tarjeta.appendChild(marco);
    tarjeta.appendChild(el("h3", "", v.titulo));
    tarjeta.appendChild(el("p", "", v.descripcion));
    cont.appendChild(tarjeta);
  });
}

/* ---------- Envío de formularios ----------
   Si hay "endpoint" configurado, envía los datos ahí. Si no, solo simula. */
async function enviarFormulario(datos, endpoint) {
  if (!endpoint) {
    await new Promise(r => setTimeout(r, 600));   // simulación
    return true;
  }
  const resp = await fetch(endpoint, {
    method: "POST",
    headers: { "Content-Type": "application/json", "Accept": "application/json" },
    body: JSON.stringify(datos)
  });
  return resp.ok;
}

function mostrarMensaje(caja, tipo, texto) {
  caja.className = "mensaje visible " + tipo;
  caja.textContent = texto;
}

/* ---------- Encuesta ---------- */
$("form-encuesta").addEventListener("submit", async (e) => {
  e.preventDefault();
  const form = e.target;
  const msg = $("msg-encuesta");
  const comprension = form.querySelector('input[name="comprension"]:checked');

  if (!comprension || !form.horario.value) {
    mostrarMensaje(msg, "error", "Por favor responde las preguntas 1 y 2 antes de enviar.");
    return;
  }

  const datos = {
    comprension: comprension.value,
    horario: form.horario.value,
    temas: [...form.querySelectorAll('input[name="temas"]:checked')].map(c => c.value)
  };

  const boton = form.querySelector("button[type=submit]");
  boton.disabled = true;
  try {
    const ok = await enviarFormulario(datos, CONFIG.endpointEncuesta);
    if (ok) {
      mostrarMensaje(msg, "ok", "¡Gracias por responder! 🎉 Tus respuestas me ayudan a mejorar el curso.");
      form.reset();
    } else {
      mostrarMensaje(msg, "error", "No se pudo enviar. Intenta de nuevo en unos minutos.");
    }
  } catch (err) {
    mostrarMensaje(msg, "error", "No se pudo enviar. Revisa tu conexión e intenta de nuevo.");
  }
  boton.disabled = false;
});

/* ---------- Buzón de dudas y sugerencias ---------- */
const campoMensaje = $("mensaje");
campoMensaje.addEventListener("input", () => {
  $("contador").textContent = campoMensaje.value.length + " / 1000 caracteres";
});

$("form-buzon").addEventListener("submit", async (e) => {
  e.preventDefault();
  const form = e.target;
  const msg = $("msg-buzon");

  if (form.mensaje.value.trim().length < 5) {
    mostrarMensaje(msg, "error", "Escribe tu mensaje antes de enviar (mínimo unas palabras).");
    campoMensaje.focus();
    return;
  }

  const datos = {
    nombre: form.nombre.value.trim() || "Anónimo",
    tipo: form.tipo.value,
    mensaje: form.mensaje.value.trim()
  };

  const boton = form.querySelector("button[type=submit]");
  boton.disabled = true;
  try {
    const ok = await enviarFormulario(datos, CONFIG.endpointBuzon);
    if (ok) {
      mostrarMensaje(msg, "ok", "¡Mensaje enviado! 💌 Gracias por escribir, lo revisaré con atención.");
      form.reset();
      $("contador").textContent = "0 / 1000 caracteres";
    } else {
      mostrarMensaje(msg, "error", "No se pudo enviar. Intenta de nuevo en unos minutos.");
    }
  } catch (err) {
    mostrarMensaje(msg, "error", "No se pudo enviar. Revisa tu conexión e intenta de nuevo.");
  }
  boton.disabled = false;
});

/* ---------- Arranque ---------- */
pintarTextosGenerales();
pintarTareas("todas");
pintarVideos();
</script>
</body>
</html>
