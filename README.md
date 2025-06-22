<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>SmartContent - Generador de contenido con IA</title>
  <style>
    /* Reset y estilos básicos */
    * {
      margin: 0; padding: 0; box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    body {
      background: #f5f7fa;
      color: #333;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }
    header {
      background: #0078d7;
      color: white;
      padding: 1rem 2rem;
      text-align: center;
      font-size: 1.8rem;
      font-weight: 700;
      letter-spacing: 1.2px;
      box-shadow: 0 3px 6px rgba(0,0,0,0.1);
    }
    main {
      flex: 1;
      max-width: 900px;
      margin: 2rem auto;
      padding: 0 1rem;
    }
    h1 {
      text-align: center;
      margin-bottom: 1rem;
      color: #0078d7;
    }
    .form-section {
      background: white;
      padding: 1.5rem 2rem;
      border-radius: 8px;
      box-shadow: 0 3px 10px rgba(0,0,0,0.05);
      margin-bottom: 2rem;
    }
    label {
      font-weight: 600;
      display: block;
      margin-bottom: 0.5rem;
    }
    select, textarea, input[type="text"] {
      width: 100%;
      padding: 0.5rem;
      margin-bottom: 1rem;
      border-radius: 5px;
      border: 1px solid #ccc;
      font-size: 1rem;
      resize: vertical;
    }
    button {
      background: #0078d7;
      border: none;
      color: white;
      padding: 0.75rem 1.5rem;
      font-size: 1.1rem;
      border-radius: 5px;
      cursor: pointer;
      transition: background 0.3s ease;
    }
    button:hover {
      background: #005ea2;
    }
    .output-section {
      background: #e8f0fe;
      padding: 1rem 1.5rem;
      border-radius: 8px;
      min-height: 100px;
      font-size: 1.1rem;
      white-space: pre-wrap;
      color: #222;
      box-shadow: inset 0 0 5px rgba(0,0,0,0.1);
    }
    footer {
      text-align: center;
      padding: 1rem;
      background: #0078d7;
      color: white;
      margin-top: auto;
      font-size: 0.9rem;
    }
    /* Responsive */
    @media (max-width: 600px) {
      main {
        margin: 1rem;
      }
      button {
        width: 100%;
      }
    }
  </style>
</head>
<body>

<header>
  SmartContent - Generador de Contenido con IA
</header>

<main>
  <h1>Genera contenido para tus redes sociales, blogs y más</h1>
  <section class="form-section">
    <label for="content-type">Selecciona el tipo de contenido:</label>
    <select id="content-type" aria-label="Tipo de contenido">
      <option value="post">Post para Instagram/Facebook</option>
      <option value="tweet">Tweet</option>
      <option value="description">Descripción de producto</option>
      <option value="email">Email profesional</option>
      <option value="blog-idea">Idea para blog</option>
      <option value="headline">Titular llamativo</option>
      <option value="ad-text">Texto para anuncio</option>
      <option value="summary">Resumen de texto</option>
    </select>

    <label for="language">Selecciona el idioma:</label>
    <select id="language" aria-label="Idioma">
      <option value="es">Español</option>
      <option value="en">Inglés</option>
    </select>

    <label for="input-text">Describe el tema o palabras clave:</label>
    <textarea id="input-text" rows="4" placeholder="Ejemplo: lanzamiento de nuevo producto tecnológico"></textarea>

    <button id="generate-btn">Generar contenido</button>
  </section>

  <section class="form-section">
    <h2>Contenido generado:</h2>
    <div id="output" class="output-section" aria-live="polite"></div>
  </section>
</main>

<footer>
  © 2025 SmartContent • <a href="mailto:contacto@smartcontent.com" style="color:#fff; text-decoration:underline;">Contacto</a>
</footer>

<script>
  const generateBtn = document.getElementById('generate-btn');
  const output = document.getElementById('output');

  // Función simulada para generar contenido (más adelante conectas API real)
  function generateContent(type, lang, text) {
    const templates = {
      es: {
        post: `Aquí tienes un post para Instagram sobre "${text}":\n\n¡Descubre todo sobre ${text} y cómo puede cambiar tu vida! #Innovación #SmartContent`,
        tweet: `Tweet sobre "${text}":\n\n¡No te pierdas las novedades de ${text}! #Trending`,
        description: `Descripción de producto para "${text}":\n\nProducto de alta calidad relacionado con ${text}, perfecto para tus necesidades.`,
        email: `Email profesional sobre "${text}":\n\nEstimado cliente,\nQueremos informarle sobre ${text} que seguro le interesará.\nSaludos cordiales.`,
        'blog-idea': `Idea para blog sobre "${text}":\n\nCómo ${text} está revolucionando la industria y lo que debes saber.`,
        headline: `Titular llamativo sobre "${text}":\n\n¡Impactante! ${text} que cambiará todo.`,
        'ad-text': `Texto para anuncio sobre "${text}":\n\nCompra ahora ${text} y aprovecha la oferta exclusiva.`,
        summary: `Resumen de texto sobre "${text}":\n\n${text} en pocas palabras para entender rápido.`,
      },
      en: {
        post: `Here is an Instagram post about "${text}":\n\nDiscover everything about ${text} and how it can change your life! #Innovation #SmartContent`,
        tweet: `Tweet about "${text}":\n\nDon't miss out on the latest about ${text}! #Trending`,
        description: `Product description for "${text}":\n\nHigh-quality product related to ${text}, perfect for your needs.`,
        email: `Professional email about "${text}":\n\nDear customer,\nWe want to inform you about ${text} that will surely interest you.\nBest regards.`,
        'blog-idea': `Blog idea about "${text}":\n\nHow ${text} is revolutionizing the industry and what you need to know.`,
        headline: `Catchy headline about "${text}":\n\nAmazing! ${text} that will change everything.`,
        'ad-text': `Ad text about "${text}":\n\nBuy now ${text} and take advantage of the exclusive offer.`,
        summary: `Summary about "${text}":\n\n${text} in a nutshell for quick understanding.`,
      }
    };

    return templates[lang][type];
  }

  generateBtn.addEventListener('click', () => {
    const type = document.getElementById('content-type').value;
    const lang = document.getElementById('language').value;
    const text = document.getElementById('input-text').value.trim();

    if (!text) {
      alert('Por favor, escribe un tema o palabras clave.');
      return;
    }

    output.textContent = 'Generando contenido...';

    // Simulación de generación con retraso
    setTimeout(() => {
      const result = generateContent(type, lang, text);
      output.textContent = result;
    }, 1000);
  });
</script>

</body>
</html>
