[index.html](https://github.com/user-attachments/files/26802861/index.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nickcel — Generador de Pagarés</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:system-ui,-apple-system,sans-serif;background:#f0f2f5;color:#1a1a1a;font-size:14px}
.app{display:grid;grid-template-columns:420px 1fr;min-height:100vh}
.panel{background:#fff;border-right:1px solid #ddd;padding:24px;overflow-y:auto}
.preview{background:#e8e8e8;padding:20px;overflow-y:auto}
.logo{background:#1e3a5f;color:#fff;padding:16px 20px;margin:-24px -24px 20px;border-radius:0}
.logo h1{font-size:15px;font-weight:700;margin-bottom:2px}
.logo p{font-size:11px;opacity:.7}
.sec-title{font-size:11px;font-weight:700;color:#666;text-transform:uppercase;letter-spacing:.06em;margin:18px 0 10px;padding-top:14px;border-top:1px solid #eee}
.sec-title:first-of-type{border-top:none;margin-top:0;padding-top:0}
.field{margin-bottom:10px}
.field label{display:block;font-size:12px;color:#555;margin-bottom:4px;font-weight:500}
.field input,.field select{width:100%;padding:8px 10px;border:1px solid #ccc;border-radius:6px;font-size:13px;font-family:inherit;outline:none;transition:border-color .15s}
.field input:focus,.field select:focus{border-color:#2e75b6}
.field input.hl{border-color:#e6a817;background:#fffbf0}
.field label.hl{color:#b06000}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.row3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px}
.calc-box{background:#f0f7ff;border:1px solid #b8d4f4;border-radius:8px;padding:14px;margin:12px 0}
.calc-title{font-size:11px;font-weight:700;color:#2e75b6;text-transform:uppercase;margin-bottom:10px}
.calc-row{display:flex;justify-content:space-between;padding:4px 0;font-size:13px;border-bottom:1px solid #dce8f5}
.calc-row:last-child{border-bottom:none;font-weight:700;color:#1e3a5f;font-size:14px;padding-top:8px;margin-top:4px}
.calc-row .val{font-weight:600;color:#1e3a5f}
.tasa-btn{display:grid;grid-template-columns:1fr 1fr 1fr;gap:6px;margin-bottom:10px}
.tb{padding:8px;border:1px solid #ccc;border-radius:6px;background:#fff;cursor:pointer;font-size:12px;text-align:center;transition:all .15s}
.tb:hover{background:#f0f7ff;border-color:#2e75b6}
.tb.active{background:#1e3a5f;color:#fff;border-color:#1e3a5f}
.tb .t-cuotas{font-weight:700;font-size:13px}
.tb .t-tasa{font-size:11px;opacity:.8}
.btn-gen{width:100%;padding:12px;background:#1e3a5f;color:#fff;border:none;border-radius:8px;font-size:14px;font-weight:600;cursor:pointer;margin-top:12px;font-family:inherit}
.btn-gen:hover{background:#2e5080}
.btn-print{padding:10px 20px;background:#1e7a4a;color:#fff;border:none;border-radius:6px;font-size:13px;font-weight:600;cursor:pointer;font-family:inherit}
.btn-print:hover{background:#155f38}
.btn-clear{padding:10px 20px;background:#fff;color:#666;border:1px solid #ccc;border-radius:6px;font-size:13px;cursor:pointer;font-family:inherit;margin-left:8px}
.preview-toolbar{display:flex;align-items:center;justify-content:space-between;margin-bottom:16px}
.preview-title{font-size:14px;font-weight:600;color:#333}

/* PAGARE STYLES */
.pagare-wrap{background:#fff;max-width:820px;margin:0 auto;box-shadow:0 2px 12px rgba(0,0,0,.15)}
.pagare{padding:20px 24px;border-bottom:3px dashed #aaa}
.pagare:last-of-type{border-bottom:none}
.p-header{background:#1e3a5f;color:#fff;padding:12px 16px;margin:-20px -24px 16px;display:flex;justify-content:space-between;align-items:center}
.p-header-left h2{font-size:14px;font-weight:700;margin-bottom:2px}
.p-header-left p{font-size:11px;opacity:.75}
.p-header-right{font-size:13px;font-weight:700;background:rgba(255,255,255,.2);padding:6px 12px;border-radius:4px}
.p-monto-box{border:2px solid #1e3a5f;border-radius:6px;padding:8px 14px;margin-bottom:14px;display:flex;justify-content:space-between;align-items:center}
.p-monto-label{font-size:11px;color:#666;text-transform:uppercase;letter-spacing:.05em}
.p-monto-val{font-size:18px;font-weight:700;color:#1e3a5f}
.p-monto-letras{font-size:12px;color:#333;font-style:italic}
.p-body{font-size:11.5px;line-height:1.7;color:#1a1a1a;margin-bottom:12px;text-align:justify}
.p-field-row{display:flex;gap:16px;margin-bottom:8px}
.p-field{flex:1}
.p-field label{font-size:10px;color:#888;text-transform:uppercase;letter-spacing:.04em;display:block;margin-bottom:1px}
.p-field .val{border-bottom:1px solid #333;padding:2px 0;font-size:12px;min-height:20px;font-weight:500}
.p-field .val.empty{color:#aaa;font-style:italic;font-weight:400}
.p-legal{font-size:10.5px;color:#444;line-height:1.6;background:#f9f9f9;padding:10px 12px;border-radius:4px;margin-bottom:12px;text-align:justify}
.p-firmas{display:grid;grid-template-columns:1fr 1fr;gap:20px;margin-top:16px}
.p-firma-box{text-align:center}
.p-firma-line{border-top:1px solid #333;padding-top:6px;font-size:11px;color:#555}

/* CUOTAS */
.cuotas-wrap{background:#fff;max-width:820px;margin:16px auto 0;box-shadow:0 2px 12px rgba(0,0,0,.15);padding:20px 24px}
.c-header{background:#1e3a5f;color:#fff;padding:10px 16px;margin:-20px -24px 16px;display:flex;justify-content:space-between}
.c-header h3{font-size:13px;font-weight:700}
.c-cliente-info{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;margin-bottom:14px}
.c-info-item label{font-size:10px;color:#888;text-transform:uppercase;display:block;margin-bottom:1px}
.c-info-item .val{font-size:13px;font-weight:600;color:#1e3a5f;border-bottom:1px solid #ddd;padding-bottom:2px}
.cuotas-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.cuotas-table{width:100%;border-collapse:collapse;font-size:12px}
.cuotas-table th{background:#1e3a5f;color:#fff;padding:6px 10px;text-align:left;font-size:11px}
.cuotas-table td{padding:5px 10px;border-bottom:1px solid #eee}
.cuotas-table tr:nth-child(even) td{background:#f5f8fc}
.cuotas-table td:last-child{text-align:right;font-weight:600}
.cuotas-table td.firma{text-align:center;color:#aaa;font-size:10px}
.resumen-caja{background:#f0f7ff;border:1px solid #b8d4f4;border-radius:6px;padding:12px;margin-top:14px}
.res-row{display:flex;justify-content:space-between;font-size:12px;padding:3px 0;border-bottom:1px solid #dce8f5}
.res-row:last-child{border-bottom:none;font-weight:700;font-size:14px;color:#1e3a5f;padding-top:6px}

@media print{
  body{background:#fff}
  .app{display:block}
  .panel{display:none}
  .preview{background:#fff;padding:0}
  .preview-toolbar{display:none}
  .pagare-wrap,.cuotas-wrap{box-shadow:none;max-width:100%}
  .pagare{page-break-inside:avoid}
  .cuotas-wrap{page-break-before:always}
}
/* CARTERA STYLES */
.main-nav{display:flex;background:#1e3a5f;padding:0 0 0 0}
.main-nav button{padding:10px 20px;border:none;background:none;color:rgba(255,255,255,.6);font-size:13px;font-weight:500;cursor:pointer;font-family:inherit;border-bottom:3px solid transparent;transition:all .15s}
.main-nav button:hover{color:#fff;background:rgba(255,255,255,.08)}
.main-nav button.active{color:#fff;border-bottom:3px solid #fff}
.screen{display:none;padding:20px;background:#f0f2f5;min-height:100vh}
.screen.active{display:block}
.search-box{background:#fff;border-radius:10px;padding:20px;margin-bottom:16px;box-shadow:0 1px 4px rgba(0,0,0,.08)}
.search-input{width:100%;padding:10px 14px;border:2px solid #ddd;border-radius:8px;font-size:15px;font-family:inherit;outline:none;transition:border-color .15s}
.search-input:focus{border-color:#1e3a5f}
.cliente-card{background:#fff;border-radius:10px;padding:18px 20px;margin-bottom:12px;box-shadow:0 1px 4px rgba(0,0,0,.08)}
.cliente-header{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:12px}
.cliente-nombre{font-size:16px;font-weight:700;color:#1e3a5f}
.cliente-dni{font-size:12px;color:#888;margin-top:2px}
.badge-ok{background:#d4f0e0;color:#1a7a4a;padding:3px 10px;border-radius:20px;font-size:11px;font-weight:700}
.badge-mora{background:#fde8e8;color:#c00;padding:3px 10px;border-radius:20px;font-size:11px;font-weight:700}
.badge-pagado{background:#e8e8e8;color:#666;padding:3px 10px;border-radius:20px;font-size:11px;font-weight:700}
.credito-row{display:flex;gap:16px;flex-wrap:wrap;margin-bottom:10px;font-size:12px}
.credito-row span{color:#555}
.credito-row strong{color:#1e3a5f}
.cuotas-estado{border-top:1px solid #eee;padding-top:10px;margin-top:6px}
.cuota-row{display:flex;align-items:center;justify-content:space-between;padding:5px 8px;border-radius:6px;margin-bottom:3px;font-size:12px}
.cuota-row.pagada{background:#f0faf5}
.cuota-row.pendiente{background:#fff9f0}
.cuota-row.vencida{background:#fdf0f0}
.cuota-row .c-num{font-weight:700;color:#1e3a5f;min-width:30px}
.cuota-row .c-fecha{color:#555;flex:1}
.cuota-row .c-monto{font-weight:600;color:#333;min-width:100px;text-align:right}
.cuota-row .c-estado{min-width:80px;text-align:right}
.btn-pagar{padding:3px 10px;border:none;border-radius:5px;background:#1e3a5f;color:#fff;font-size:11px;cursor:pointer;font-family:inherit}
.btn-pagar:hover{background:#2e5080}
.empty-state{text-align:center;padding:40px;color:#999;font-size:14px}
</style>
<style>
.login-screen{display:flex;align-items:center;justify-content:center;min-height:100vh;background:#f0f2f5}
.login-box{background:#fff;border-radius:12px;padding:32px 28px;width:100%;max-width:320px;box-shadow:0 4px 20px rgba(0,0,0,.12);text-align:center}
.login-box h2{font-size:17px;font-weight:700;color:#1e3a5f;margin-bottom:4px}
.login-box p{font-size:12px;color:#888;margin-bottom:20px}
.login-inp{width:100%;padding:10px 12px;border:1px solid #ddd;border-radius:7px;font-size:14px;font-family:inherit;outline:none;margin-bottom:8px;transition:border-color .15s}
.login-inp:focus{border-color:#1e3a5f}
.login-btn-main{width:100%;padding:11px;background:#1e3a5f;color:#fff;border:none;border-radius:8px;font-size:14px;font-weight:600;cursor:pointer;font-family:inherit}
.login-btn-main:hover{background:#2e5080}
.login-err{font-size:12px;color:#c00;min-height:16px;margin-bottom:8px}
</style>
</head>
<body>

<!-- LOGIN -->
<div id="login-screen" class="login-screen">
  <div class="login-box">
    <div style="font-size:32px;margin-bottom:10px">🏪</div>
    <h2>NICKCEL TECNO & HOGAR</h2>
    <p>Ingresá tu contraseña para continuar</p>
    <input type="password" id="inp-login-pass" class="login-inp" placeholder="Contraseña" onkeydown="if(event.key==='Enter')doLogin()">
    <div id="login-err" class="login-err"></div>
    <button class="login-btn-main" onclick="doLogin()">Ingresar</button>
  </div>
</div>

<!-- APP PRINCIPAL -->
<div id="main-app" style="display:none">
<div class="main-nav" id="main-nav">
  <button class="active" onclick="showScreen('pagare',this)">Nuevo Pagaré</button>
  <button onclick="showScreen('cartera',this)">Cartera de Clientes</button>
  <div style="margin-left:auto;display:flex;align-items:center;padding-right:14px;gap:10px">
    <span id="rol-indicator" style="font-size:11px;font-weight:700;padding:2px 10px;border-radius:20px;background:rgba(255,255,255,.15);color:#fff"></span>
    <button onclick="doLogout()" style="padding:5px 12px;border:1px solid rgba(255,255,255,.3);border-radius:6px;background:transparent;color:rgba(255,255,255,.8);font-size:11px;cursor:pointer;font-family:inherit">Salir</button>
  </div>
</div>

<!-- SCREEN: PAGARE -->
<div id="screen-pagare" class="screen active" style="padding:0;background:none">
<div class="app">

<!-- PANEL IZQUIERDO -->
<div class="panel">
  <div class="logo">
    <h1>NICKCEL TECNO & HOGAR S.R.L.</h1>
    <p>Generador de Pagarés — CUIT 30-71899140-0 | Quitilipi, Chaco</p>
  </div>

  <div class="sec-title">Datos del cliente</div>

  <!-- TABS -->
  <div style="display:flex;gap:0;margin-bottom:12px;border-bottom:2px solid #ddd">
    <button onclick="showTab('cliente',this)" id="tab-btn-cliente" style="padding:7px 14px;border:none;background:none;font-size:12px;font-weight:700;color:#1e3a5f;border-bottom:2px solid #1e3a5f;margin-bottom:-2px;cursor:pointer;font-family:inherit">Cliente</button>
    <button onclick="showTab('fam1',this)" id="tab-btn-fam1" style="padding:7px 14px;border:none;background:none;font-size:12px;font-weight:400;color:#888;cursor:pointer;font-family:inherit">Familiar 1</button>
    <button onclick="showTab('fam2',this)" id="tab-btn-fam2" style="padding:7px 14px;border:none;background:none;font-size:12px;font-weight:400;color:#888;cursor:pointer;font-family:inherit">Familiar 2</button>
  </div>

  <!-- TAB CLIENTE -->
  <div id="tab-cliente">
    <div class="field"><label>Nombre y Apellido</label><input type="text" id="nombre" placeholder="Ej: Garcia Juan Carlos"></div>
    <div class="row2">
      <div class="field"><label>DNI</label><input type="text" id="dni" placeholder="Ej: 28123456"></div>
      <div class="field"><label>
        Teléfono principal
        <span id="tel-status" style="margin-left:6px;font-size:10px;color:#888"></span>
      </label>
        <div style="display:flex;gap:6px">
          <input type="text" id="tel" placeholder="Ej: 3624-123456" style="flex:1">
          <button onclick="verificarTel()" style="padding:0 10px;background:#1e3a5f;color:#fff;border:none;border-radius:6px;font-size:11px;cursor:pointer;white-space:nowrap">Verificar</button>
        </div>
      </div>
    </div>
    <!-- Código de verificación -->
    <div id="verify-box" style="display:none;background:#fffbf0;border:1px solid #e6a817;border-radius:6px;padding:10px;margin-bottom:8px">
      <div style="font-size:12px;color:#b06000;margin-bottom:6px">
        Código generado: <strong id="codigo-generado" style="font-size:16px;letter-spacing:3px;color:#1e3a5f"></strong>
        <span style="font-size:11px;color:#888"> — mandalo por WhatsApp al cliente</span>
      </div>
      <div style="display:flex;gap:6px">
        <input type="text" id="codigo-input" placeholder="Ingresá el código que respondió" style="flex:1;font-size:13px;letter-spacing:2px">
        <button onclick="confirmarCodigo()" style="padding:0 12px;background:#1a7a4a;color:#fff;border:none;border-radius:6px;font-size:11px;cursor:pointer">Confirmar</button>
      </div>
      <div id="verify-msg" style="font-size:11px;margin-top:4px"></div>
    </div>
    <div class="field"><label>Domicilio</label><input type="text" id="domicilio" placeholder="Calle y número"></div>
    <div class="row2">
      <div class="field"><label>Localidad</label><input type="text" id="localidad" placeholder="Ej: Resistencia"></div>
      <div class="field"><label>CUIT (opcional)</label><input type="text" id="cuit" placeholder="Ej: 20-28123456-3"></div>
    </div>
  </div>

  <!-- TAB FAMILIAR 1 -->
  <div id="tab-fam1" style="display:none">
    <div style="background:#f0f7ff;border-radius:6px;padding:8px 12px;margin-bottom:10px;font-size:12px;color:#2e75b6">
      Referencia familiar — se incluye en el pagaré como contacto adicional
    </div>
    <div class="field"><label>Nombre y Apellido</label><input type="text" id="fam1-nombre" placeholder="Ej: Garcia Pedro"></div>
    <div class="row2">
      <div class="field"><label>DNI</label><input type="text" id="fam1-dni" placeholder="Ej: 30456789"></div>
      <div class="field"><label>Teléfono</label><input type="text" id="fam1-tel" placeholder="Ej: 3624-654321"></div>
    </div>
    <div class="field"><label>Domicilio</label><input type="text" id="fam1-dom" placeholder="Calle y número"></div>
    <div class="row2">
      <div class="field"><label>Localidad</label><input type="text" id="fam1-loc" placeholder="Ej: Resistencia"></div>
      <div class="field"><label>Relación con el cliente</label>
        <select id="fam1-rel">
          <option>Cónyuge</option><option>Padre/Madre</option><option>Hijo/a</option>
          <option>Hermano/a</option><option>Otro familiar</option>
        </select>
      </div>
    </div>
  </div>

  <!-- TAB FAMILIAR 2 -->
  <div id="tab-fam2" style="display:none">
    <div style="background:#f0f7ff;border-radius:6px;padding:8px 12px;margin-bottom:10px;font-size:12px;color:#2e75b6">
      Referencia familiar — se incluye en el pagaré como contacto adicional
    </div>
    <div class="field"><label>Nombre y Apellido</label><input type="text" id="fam2-nombre" placeholder="Ej: Garcia Ana"></div>
    <div class="row2">
      <div class="field"><label>DNI</label><input type="text" id="fam2-dni" placeholder="Ej: 32456789"></div>
      <div class="field"><label>Teléfono</label><input type="text" id="fam2-tel" placeholder="Ej: 3624-789012"></div>
    </div>
    <div class="field"><label>Domicilio</label><input type="text" id="fam2-dom" placeholder="Calle y número"></div>
    <div class="row2">
      <div class="field"><label>Localidad</label><input type="text" id="fam2-loc" placeholder="Ej: Resistencia"></div>
      <div class="field"><label>Relación con el cliente</label>
        <select id="fam2-rel">
          <option>Cónyuge</option><option>Padre/Madre</option><option>Hijo/a</option>
          <option>Hermano/a</option><option>Otro familiar</option>
        </select>
      </div>
    </div>
  </div>

  <div class="sec-title">Crédito</div>
  <div class="field"><label class="hl">Monto a financiar ($)</label><input type="number" id="monto" class="hl" placeholder="Ej: 300000" oninput="calcular()"></div>
  <div class="row2">
    <div class="field"><label>Precio contado ($)</label><input type="number" id="contado" placeholder="Ej: 250000"></div>
    <div class="field"><label>Fecha 1° cuota</label><input type="date" id="fecha1"></div>
  </div>

  <div class="sec-title">Seleccionar plan de cuotas</div>
  <div class="tasa-btn" id="planes-btn"></div>

  <div class="field">
    <label>O ingresá manualmente:</label>
    <div class="row2">
      <div class="field"><label>N° cuotas</label><input type="number" id="ncuotas" placeholder="Máx. 12" min="1" max="12" oninput="calcularManual()"></div>
      <div class="field"><label>Tasa mensual (%)</label><input type="number" id="tasa" placeholder="Ej: 9.2" step="0.1" oninput="calcularManual()"></div>
    </div>
  </div>

  <div class="calc-box" id="calc-box" style="display:none">
    <div class="calc-title">Resumen del crédito</div>
    <div class="calc-row"><span>Monto financiado</span><span class="val" id="c-monto">-</span></div>
    <div class="calc-row"><span>Cuota mensual</span><span class="val" id="c-cuota">-</span></div>
    <div class="calc-row"><span>Tasa mensual</span><span class="val" id="c-tasa">-</span></div>
    <div class="calc-row"><span>Tasa anual (T.E.A.)</span><span class="val" id="c-tea">-</span></div>
    <div class="calc-row"><span>Total a devolver</span><span class="val" id="c-total">-</span></div>
    <div class="calc-row"><span>Interés total</span><span class="val" id="c-interes">-</span></div>
    <div class="calc-row"><span>TOTAL CON SEGURO</span><span class="val" id="c-total-seg">-</span></div>
  </div>

  <div class="field" style="margin-top:8px">
    <label>Seguro de vida ($ por cuota)</label>
    <input type="number" id="seguro" placeholder="0" value="0" oninput="calcular()">
  </div>
  <div class="field">
    <label>N° de crédito (opcional)</label>
    <input type="text" id="ncredito" placeholder="Se genera automático si está vacío">
  </div>

  <button class="btn-gen" onclick="generar()">Generar Pagaré</button>
</div>

<!-- PANEL DERECHO — PREVIEW -->
<div class="preview">
  <div class="preview-toolbar">
    <div class="preview-title" id="prev-title">Complete los datos y presione "Generar Pagaré"</div>
    <div>
      <button class="btn-print" onclick="window.print()">Imprimir / Guardar PDF</button>
      <button class="btn-clear" onclick="limpiar()">Nuevo</button>
    </div>
  </div>
  <div id="preview-content">
    <div style="text-align:center;padding:60px 20px;color:#999;font-size:14px">
      Complete los datos del cliente y el monto para generar el pagaré
    </div>
  </div>
</div>

</div>

</div><!-- /app -->
</div><!-- /screen-pagare -->

<!-- SCREEN: CARTERA -->
<div id="screen-cartera" class="screen">
  <div class="search-box">
    <div style="font-size:16px;font-weight:700;color:#1e3a5f;margin-bottom:12px">Cartera de clientes</div>
    <input type="text" class="search-input" id="buscar-dni" placeholder="Buscar por DNI, nombre o N° crédito..." oninput="buscarCliente()">
    <div style="display:flex;gap:8px;margin-top:10px;flex-wrap:wrap">
      <button onclick="filtrarCartera('todos')" id="f-todos" style="padding:6px 14px;border:1px solid #1e3a5f;border-radius:20px;background:#1e3a5f;color:#fff;font-size:12px;cursor:pointer;font-family:inherit">Todos</button>
      <button onclick="filtrarCartera('mora')" id="f-mora" style="padding:6px 14px;border:1px solid #ccc;border-radius:20px;background:#fff;color:#555;font-size:12px;cursor:pointer;font-family:inherit">En mora</button>
      <button onclick="filtrarCartera('activo')" id="f-activo" style="padding:6px 14px;border:1px solid #ccc;border-radius:20px;background:#fff;color:#555;font-size:12px;cursor:pointer;font-family:inherit">Al día</button>
      <button onclick="filtrarCartera('pagado')" id="f-pagado" style="padding:6px 14px;border:1px solid #ccc;border-radius:20px;background:#fff;color:#555;font-size:12px;cursor:pointer;font-family:inherit">Cancelados</button>
    </div>
  </div>
  <div id="cartera-stats" style="display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:14px"></div>
  <div id="cartera-lista"></div>
</div>

<script type="module">
// =========================================================
// FIREBASE CONFIG
// =========================================================
import { initializeApp } from "https://www.gstatic.com/firebasejs/12.12.0/firebase-app.js";
import { getFirestore, collection, doc, setDoc, getDocs, updateDoc, deleteDoc, query, orderBy } from "https://www.gstatic.com/firebasejs/12.12.0/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "AIzaSyAhBYwPQJ2MU2U4wFdu58JS826dOV1-h9c",
  authDomain: "nickcel-pagares.firebaseapp.com",
  projectId: "nickcel-pagares",
  storageBucket: "nickcel-pagares.firebasestorage.app",
  messagingSenderId: "235121339876",
  appId: "1:235121339876:web:981870b479117906822bf1",
  measurementId: "G-VXTTQM9X9Z"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

// Estado global en memoria
let carteraCache = [];
let cargando = false;
window._carteraCache = carteraCache;

function mostrarCargando(msg) {
  document.getElementById('cartera-lista').innerHTML = `<div class="empty-state">${msg||'Cargando...'}</div>`;
}

// =========================================================
// NAVEGACION PRINCIPAL
// =========================================================
window.showScreen = function(s, btn){
  document.querySelectorAll('.screen').forEach(el=>el.classList.remove('active'));
  document.querySelectorAll('.main-nav button').forEach(b=>{b.classList.remove('active');});
  document.getElementById('screen-'+s).classList.add('active');
  btn.classList.add('active');
  if(s==='cartera') cargarYRenderCartera('todos');
}

// =========================================================
// FIREBASE — CARGAR CARTERA
// =========================================================
async function cargarCartera(){
  const snap = await getDocs(query(collection(db,'creditos'), orderBy('fechaEmision','desc')));
  carteraCache = [];
  snap.forEach(d => carteraCache.push({...d.data(), _id: d.id}));
  return carteraCache;
}

async function cargarYRenderCartera(filtro){
  mostrarCargando('Cargando cartera...');
  await cargarCartera();
  renderCartera(filtro||filtroActual);
}

// =========================================================
// GUARDAR CREDITO AL GENERAR PAGARE
// =========================================================
window.guardarCredito = async function(datos){
  try {
    await setDoc(doc(db, 'creditos', datos.ncredito), datos);
    carteraCache.unshift({...datos, _id: datos.ncredito});
  } catch(e) {
    console.error('Error guardando en Firebase:', e);
    alert('Error al guardar en la nube. Verificá tu conexión.');
  }
}

// =========================================================
// RENDER CARTERA
// =========================================================
let filtroActual = 'todos';
let busquedaActual = '';

function estadoCredito(credito){
  const hoy = new Date();
  hoy.setHours(0,0,0,0);
  const cuotasPendientes = credito.cuotas.filter(c=>!c.pagada);
  if(cuotasPendientes.length===0) return 'pagado';
  const vencidas = credito.cuotas.filter(c=>!c.pagada && new Date(c.fechaISO) < hoy);
  if(vencidas.length>0) return 'mora';
  return 'activo';
}

function diasMora(credito){
  const hoy = new Date(); hoy.setHours(0,0,0,0);
  const vencidas = credito.cuotas.filter(c=>!c.pagada && new Date(c.fechaISO) < hoy);
  if(!vencidas.length) return 0;
  const masVieja = vencidas.reduce((a,b)=>new Date(a.fechaISO)<new Date(b.fechaISO)?a:b);
  return Math.floor((hoy-new Date(masVieja.fechaISO))/(1000*60*60*24));
}

function renderCartera(filtro){
  filtroActual = filtro;
  window._filtroActual = filtro;
  document.querySelectorAll('[id^="f-"]').forEach(b=>{
    b.style.background='#fff'; b.style.color='#555'; b.style.borderColor='#ccc';
  });
  const fb = document.getElementById('f-'+filtro);
  if(fb){ fb.style.background='#1e3a5f'; fb.style.color='#fff'; fb.style.borderColor='#1e3a5f'; }

  const cartera = carteraCache;
  const busq = busquedaActual.toLowerCase();

  let lista = cartera.filter(c=>{
    const matchBusq = !busq || c.nombre.toLowerCase().includes(busq) || c.dni.includes(busq) || c.ncredito.toLowerCase().includes(busq);
    const estado = estadoCredito(c);
    const matchFiltro = filtro==='todos' || estado===filtro;
    return matchBusq && matchFiltro;
  });

  // Stats
  const todos = cartera;
  const enMora = todos.filter(c=>estadoCredito(c)==='mora').length;
  const alDia  = todos.filter(c=>estadoCredito(c)==='activo').length;
  const pagados= todos.filter(c=>estadoCredito(c)==='pagado').length;
  const montoMora = cartera.filter(c=>estadoCredito(c)==='mora').reduce((a,c)=>{
    return a + c.cuotas.filter(q=>!q.pagada).reduce((s,q)=>s+q.monto,0);
  },0);

  document.getElementById('cartera-stats').innerHTML = `
    <div style="background:#fff;border-radius:8px;padding:12px 14px;box-shadow:0 1px 4px rgba(0,0,0,.08)">
      <div style="font-size:11px;color:#888;margin-bottom:4px">Total clientes</div>
      <div style="font-size:22px;font-weight:700;color:#1e3a5f">${todos.length}</div>
    </div>
    <div style="background:#fff;border-radius:8px;padding:12px 14px;box-shadow:0 1px 4px rgba(0,0,0,.08)">
      <div style="font-size:11px;color:#888;margin-bottom:4px">En mora</div>
      <div style="font-size:22px;font-weight:700;color:#c00">${enMora}</div>
    </div>
    <div style="background:#fff;border-radius:8px;padding:12px 14px;box-shadow:0 1px 4px rgba(0,0,0,.08)">
      <div style="font-size:11px;color:#888;margin-bottom:4px">Al día</div>
      <div style="font-size:22px;font-weight:700;color:#1a7a4a">${alDia}</div>
    </div>
    <div style="background:#fff;border-radius:8px;padding:12px 14px;box-shadow:0 1px 4px rgba(0,0,0,.08)">
      <div style="font-size:11px;color:#888;margin-bottom:4px">Deuda en mora</div>
      <div style="font-size:16px;font-weight:700;color:#c00">$${Math.round(montoMora).toLocaleString('es-AR')}</div>
    </div>`;

  const lista_html = document.getElementById('cartera-lista');
  if(!lista.length){
    lista_html.innerHTML = '<div class="empty-state">No hay clientes que coincidan con la búsqueda.</div>';
    return;
  }

  lista_html.innerHTML = lista.map((c,idx)=>{
    const estado = estadoCredito(c);
    const mora = diasMora(c);
    const cuotasPag = c.cuotas.filter(q=>q.pagada).length;
    const cuotasTot = c.cuotas.length;
    const badge = estado==='mora'
      ? `<span class="badge-mora">EN MORA ${mora} días</span>`
      : estado==='pagado'
      ? `<span class="badge-pagado">CANCELADO</span>`
      : `<span class="badge-ok">AL DÍA</span>`;

    const cuotasHtml = c.cuotas.map((q,qi)=>{
      const hoy = new Date(); hoy.setHours(0,0,0,0);
      const fVenc = new Date(q.fechaISO);
      let cls = q.pagada ? 'pagada' : fVenc < hoy ? 'vencida' : 'pendiente';
      const estadoLabel = q.pagada
        ? `<span style="color:#1a7a4a;font-size:11px">✓ Pagada ${q.fechaPago?'('+q.fechaPago+')':''}</span>`
        : fVenc < hoy
        ? `<span style="color:#c00;font-size:11px">Vencida</span>`
        : `<span style="color:#b06000;font-size:11px">Pendiente</span>`;
      const btnPagar = !q.pagada
        ? `<button class="btn-pagar" onclick="marcarPagada('${c.ncredito}',${qi})">Cobrar</button>`
        : (window.rolActual === 'admin' ? `<button onclick="anularCuota('${c.ncredito}',${qi})" style="padding:3px 10px;border:none;border-radius:5px;background:#c00;color:#fff;font-size:11px;cursor:pointer;font-family:inherit">Anular</button>` : '');
      return `<div class="cuota-row ${cls}">
        <span class="c-num">${q.num}</span>
        <span class="c-fecha">${q.fecha}</span>
        <span class="c-monto">$${Math.round(q.monto).toLocaleString('es-AR')}</span>
        <span class="c-estado">${estadoLabel}</span>
        <span>${btnPagar}</span>
      </div>`;
    }).join('');

    return `<div class="cliente-card">
      <div class="cliente-header">
        <div>
          <div class="cliente-nombre">${c.nombre}</div>
          <div class="cliente-dni">DNI: ${c.dni} &nbsp;|&nbsp; Tel: ${c.tel||'—'} &nbsp;|&nbsp; N° Crédito: ${c.ncredito}</div>
        </div>
        <div style="display:flex;gap:8px;align-items:center">
          ${badge}
          <button onclick="toggleDetalle('det-${c.ncredito}')" style="padding:4px 10px;border:1px solid #ccc;border-radius:6px;background:#fff;font-size:11px;cursor:pointer;font-family:inherit">Ver cuotas</button>
          ${window.rolActual==='admin'?`<button onclick="eliminarCredito('${c.ncredito}')" style="padding:4px 8px;border:1px solid #f5c0c0;border-radius:6px;background:#fff;color:#c00;font-size:11px;cursor:pointer;font-family:inherit">×</button>`:''}
        </div>
      </div>
      <div class="credito-row">
        <span>Monto: <strong>$${Math.round(c.monto).toLocaleString('es-AR')}</strong></span>
        <span>Cuotas: <strong>${cuotasPag}/${cuotasTot} pagadas</strong></span>
        <span>Cuota: <strong>$${Math.round(c.cuotaMonto).toLocaleString('es-AR')}</strong></span>
        <span>Fecha: <strong>${c.fechaEmision}</strong></span>
      </div>
      <div class="cuotas-estado" id="det-${c.ncredito}" style="display:none">
        ${cuotasHtml}
      </div>
    </div>`;
  }).join('');
}

window.toggleDetalle = function(id){
  const el = document.getElementById(id);
  el.style.display = el.style.display==='none' ? 'block' : 'none';
}

window.marcarPagada = async function(ncredito, qi){
  const cred = carteraCache.find(c=>c.ncredito===ncredito);
  if(!cred) return;
  const fechaPago = new Date().toLocaleDateString('es-AR');
  cred.cuotas[qi].pagada = true;
  cred.cuotas[qi].fechaPago = fechaPago;
  try {
    await updateDoc(doc(db,'creditos',ncredito), { cuotas: cred.cuotas });
    renderCartera(filtroActual);
    // Generar comprobante de pago de cuota
    generarComprobanteCuota(cred, qi, fechaPago);
  } catch(e) {
    alert('Error al actualizar. Verificá tu conexión.');
  }
}

function generarComprobanteCuota(cred, qi, fechaPago) {
  const cuota = cred.cuotas[qi];
  const cuotasPagadas = cred.cuotas.filter(q=>q.pagada).length;
  const saldoRestante = cred.cuotas.filter(q=>!q.pagada).reduce((s,q)=>s+q.monto,0);
  const totalCredito = cred.cuotas.reduce((s,q)=>s+q.monto,0);
  const nroComp = `${cred.ncredito}-C${String(cuota.num).padStart(2,'0')}`;

  const html = `
  <div style="font-family:Arial,sans-serif;color:#111;background:#fff;padding:20px 24px;max-width:720px;margin:0 auto;box-shadow:0 2px 12px rgba(0,0,0,.15)">
    <div style="border-bottom:3px solid #1e3a5f;padding-bottom:12px;margin-bottom:14px;display:flex;justify-content:space-between;align-items:center">
      <div>
        <div style="font-size:18px;font-weight:700;color:#1e3a5f">NICKCEL TECNO &amp; HOGAR</div>
        <div style="font-size:11px;color:#555">San Martín 514, Quitilipi, Chaco | WhatsApp: 3644924970</div>
      </div>
      <div style="text-align:right">
        <div style="font-size:10px;color:#888;text-transform:uppercase;letter-spacing:1px">Comprobante N°</div>
        <div style="font-size:20px;font-weight:700;color:#1e3a5f">${nroComp}</div>
        <div style="font-size:11px;color:#666">Fecha: ${fechaPago}</div>
      </div>
    </div>

    <div style="background:#1e3a5f;color:#fff;text-align:center;padding:7px;font-size:13px;font-weight:700;letter-spacing:2px;text-transform:uppercase;margin-bottom:14px;border-radius:3px">
      RECIBO DE PAGO DE CUOTA
    </div>

    <div style="margin-bottom:12px">
      <div style="font-size:10px;font-weight:700;color:#1e3a5f;text-transform:uppercase;letter-spacing:1px;border-bottom:1px solid #dde3f0;padding-bottom:4px;margin-bottom:8px">Datos del cliente</div>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px 20px;font-size:13px">
        <div><div style="font-size:10px;color:#888;text-transform:uppercase">Nombre y apellido</div><div style="font-weight:600;border-bottom:1px solid #eee;padding-bottom:2px">${cred.nombre}</div></div>
        <div><div style="font-size:10px;color:#888;text-transform:uppercase">DNI</div><div style="font-weight:600;border-bottom:1px solid #eee;padding-bottom:2px">${cred.dni}</div></div>
        <div><div style="font-size:10px;color:#888;text-transform:uppercase">Teléfono</div><div style="font-weight:600;border-bottom:1px solid #eee;padding-bottom:2px">${cred.tel||'—'}</div></div>
        <div><div style="font-size:10px;color:#888;text-transform:uppercase">N° Crédito</div><div style="font-weight:600;border-bottom:1px solid #eee;padding-bottom:2px">${cred.ncredito}</div></div>
      </div>
    </div>

    <div style="margin-bottom:12px">
      <div style="font-size:10px;font-weight:700;color:#1e3a5f;text-transform:uppercase;letter-spacing:1px;border-bottom:1px solid #dde3f0;padding-bottom:4px;margin-bottom:8px">Detalle del pago</div>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px 20px;font-size:13px">
        <div><div style="font-size:10px;color:#888;text-transform:uppercase">Concepto</div><div style="font-weight:600;border-bottom:1px solid #eee;padding-bottom:2px">Cuota N° ${cuota.num} de ${cred.cuotas.length}</div></div>
        <div><div style="font-size:10px;color:#888;text-transform:uppercase">Vencimiento</div><div style="font-weight:600;border-bottom:1px solid #eee;padding-bottom:2px">${cuota.fecha}</div></div>
        <div><div style="font-size:10px;color:#888;text-transform:uppercase">Cuotas pagadas</div><div style="font-weight:600;border-bottom:1px solid #eee;padding-bottom:2px">${cuotasPagadas} de ${cred.cuotas.length}</div></div>
        <div><div style="font-size:10px;color:#888;text-transform:uppercase">Saldo restante</div><div style="font-weight:600;border-bottom:1px solid #eee;padding-bottom:2px;color:${saldoRestante>0?'#b06000':'#1a7a4a'}">$${Math.round(saldoRestante).toLocaleString('es-AR')}</div></div>
      </div>
    </div>

    <div style="background:#f0f4fb;border:2px solid #1e3a5f;border-radius:6px;padding:12px 16px;display:flex;justify-content:space-between;align-items:center;margin:14px 0">
      <div>
        <div style="font-size:12px;color:#1e3a5f;font-weight:600;text-transform:uppercase;letter-spacing:1px">Monto abonado</div>
        <div style="font-size:10px;color:#1e3a5f;margin-top:2px;font-style:italic">${numeroALetras(cuota.monto)} pesos</div>
      </div>
      <div style="font-size:26px;font-weight:700;color:#1e3a5f">$${Math.round(cuota.monto).toLocaleString('es-AR')}</div>
    </div>

    ${saldoRestante===0?`<div style="background:#e6f4ec;border:1px solid #8ecfa8;border-radius:6px;padding:8px 14px;text-align:center;font-size:13px;font-weight:600;color:#1a7a4a;margin-bottom:12px">✓ CRÉDITO TOTALMENTE CANCELADO</div>`:''}

    <div style="border-top:1px dashed #ccc;margin-top:16px;padding-top:12px;display:grid;grid-template-columns:1fr 1fr;gap:20px">
      <div style="text-align:center"><div style="border-top:1px solid #333;width:160px;margin:40px auto 4px"></div><div style="font-size:10px;color:#555">Firma del cliente</div></div>
      <div style="text-align:center"><div style="border-top:1px solid #333;width:160px;margin:40px auto 4px"></div><div style="font-size:10px;color:#555">Firma y sello — NICKCEL</div></div>
    </div>
    <div style="text-align:center;margin-top:10px;font-size:10px;color:#999">Conserve este comprobante — NICKCEL Tecno &amp; Hogar — Quitilipi, Chaco — ${fechaPago}</div>
  </div>`;

  // Mostrar modal con comprobante
  let modal = document.getElementById('comp-cuota-modal');
  if(!modal) {
    modal = document.createElement('div');
    modal.id = 'comp-cuota-modal';
    modal.style.cssText = 'position:fixed;inset:0;background:rgba(0,0,0,0.6);z-index:9999;display:flex;align-items:center;justify-content:center;padding:20px';
    modal.innerHTML = `
      <div style="background:#fff;border-radius:12px;max-width:760px;width:100%;max-height:90vh;overflow-y:auto;box-shadow:0 40px 100px rgba(0,0,0,0.5)">
        <div style="display:flex;justify-content:space-between;align-items:center;padding:14px 20px;border-bottom:1px solid #eee">
          <span style="font-size:15px;font-weight:600;color:#1e3a5f">Comprobante de pago</span>
          <div style="display:flex;gap:8px">
            <button onclick="window.print()" style="padding:8px 16px;background:#1e3a5f;color:#fff;border:none;border-radius:6px;font-size:13px;font-weight:600;cursor:pointer">Imprimir / PDF</button>
            <button onclick="document.getElementById('comp-cuota-modal').style.display='none'" style="padding:8px 12px;background:#f0f0f0;border:none;border-radius:6px;font-size:13px;cursor:pointer">✕</button>
          </div>
        </div>
        <div id="comp-cuota-body" style="padding:20px"></div>
      </div>`;
    document.body.appendChild(modal);
  }
  modal.style.display = 'flex';
  document.getElementById('comp-cuota-body').innerHTML = html;
}

window.eliminarCredito = async function(ncredito){
  if(!confirm('¿Eliminar este crédito?')) return;
  try {
    await deleteDoc(doc(db,'creditos',ncredito));
    carteraCache = carteraCache.filter(c=>c.ncredito!==ncredito);
    window._carteraCache = carteraCache;
    renderCartera(filtroActual);
  } catch(e) {
    alert('Error al eliminar. Verificá tu conexión.');
  }
}

// Exponer funciones al scope global para acceso cross-script
window._updateCuotas = async function(ncredito, cuotas) {
  await updateDoc(doc(db,'creditos',ncredito), { cuotas });
  const cred = carteraCache.find(c=>c.ncredito===ncredito);
  if(cred) cred.cuotas = cuotas;
  window._carteraCache = carteraCache;
}
window._renderCarteraFn = function(f) { renderCartera(f); }
window._filtroActual = 'todos';

window.buscarCliente = function(){
  busquedaActual = document.getElementById('buscar-dni').value;
  renderCartera(filtroActual);
}

window.filtrarCartera = function(f){ renderCartera(f); }


// TAB NAVIGATION
window.showTab = function showTab(tab, btn){
  ['cliente','fam1','fam2'].forEach(t=>{
    document.getElementById('tab-'+t).style.display = t===tab?'block':'none';
  });
  document.querySelectorAll('[id^="tab-btn-"]').forEach(b=>{
    b.style.fontWeight='400'; b.style.color='#888'; b.style.borderBottom='2px solid transparent';
  });
  btn.style.fontWeight='700'; btn.style.color='#1e3a5f'; btn.style.borderBottom='2px solid #1e3a5f';
}

// VERIFICACION MANUAL
let codigoActual = null;
let telVerificado = false;

window.verificarTel = function(){
  const tel = document.getElementById('tel').value.trim();
  if(!tel){ alert('Ingresá el teléfono primero.'); return; }
  codigoActual = String(Math.floor(100000 + Math.random()*900000));
  document.getElementById('codigo-generado').textContent = codigoActual;
  document.getElementById('verify-box').style.display = 'block';
  document.getElementById('codigo-input').value = '';
  document.getElementById('verify-msg').innerHTML = '';
  document.getElementById('tel-status').innerHTML = '<span style="color:#b06000">⏳ pendiente</span>';
  telVerificado = false;
}

window.confirmarCodigo = function(){
  const ingresado = document.getElementById('codigo-input').value.trim();
  if(ingresado === codigoActual){
    document.getElementById('verify-msg').innerHTML = '<span style="color:#1a7a4a">✓ Teléfono verificado correctamente</span>';
    document.getElementById('tel-status').innerHTML = '<span style="color:#1a7a4a">✓ verificado</span>';
    document.getElementById('verify-box').style.display = 'none';
    telVerificado = true;
  } else {
    document.getElementById('verify-msg').innerHTML = '<span style="color:#c00">✗ Código incorrecto, intentá de nuevo</span>';
  }
}

// Tasas reales del mercado (financiera): 13.78% mensual en 12 cuotas (extraído de pagaré real)
// Vos cobrás 2% menos en cada plan
const PLANES = [
  { cuotas: 3,  tasa: 12.39, label: "3 cuotas" },
  { cuotas: 6,  tasa: 12.84, label: "6 cuotas" },
  { cuotas: 9,  tasa: 12.42, label: "9 cuotas" },
  { cuotas: 12, tasa: 11.28, label: "12 cuotas" },
];

let planActivo = null;

// Render botones de planes
const btnContainer = document.getElementById('planes-btn');
PLANES.forEach((p, i) => {
  const btn = document.createElement('button');
  btn.className = 'tb';
  btn.innerHTML = `<div class="t-cuotas">${p.cuotas} cuotas</div><div class="t-tasa">${p.tasa}% mensual</div>`;
  btn.onclick = () => seleccionarPlan(i, btn);
  btnContainer.appendChild(btn);
});

// Fecha default primer cuota — próximo mes día 1
const hoy = new Date();
// Primera cuota siempre en el día de la firma
const prox = new Date();
document.getElementById('fecha1').value = prox.toISOString().split('T')[0];

window.seleccionarPlan = function seleccionarPlan(idx, btn) {
  document.querySelectorAll('.tb').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  planActivo = PLANES[idx];
  document.getElementById('ncuotas').value = planActivo.cuotas;
  document.getElementById('tasa').value = planActivo.tasa;
  calcular();
}

window.calcularManual = function() {
  planActivo = null;
  document.querySelectorAll('.tb').forEach(b => b.classList.remove('active'));
  calcular();
}

window.calcular = function calcular() {
  const monto = parseFloat(document.getElementById('monto').value) || 0;
  const n     = parseInt(document.getElementById('ncuotas').value) || 0;
  const tasa  = parseFloat(document.getElementById('tasa').value) / 100 || 0;
  const seguro= parseFloat(document.getElementById('seguro').value) || 0;
  if (!monto || !n || !tasa) {
    document.getElementById('calc-box').style.display = 'none';
    return;
  }
  const cuota = monto * (tasa * Math.pow(1+tasa,n)) / (Math.pow(1+tasa,n)-1);
  const cuotaConSeg = cuota + seguro;
  const total = cuota * n;
  const totalConSeg = cuotaConSeg * n;
  const interes = total - monto;
  const tea = (Math.pow(1+tasa,12)-1)*100;

  document.getElementById('c-monto').textContent   = fmtP(monto);
  document.getElementById('c-cuota').textContent   = fmtP(Math.round(cuota));
  document.getElementById('c-tasa').textContent    = (tasa*100).toFixed(2)+'%';
  document.getElementById('c-tea').textContent     = tea.toFixed(1)+'%';
  document.getElementById('c-total').textContent   = fmtP(Math.round(total));
  document.getElementById('c-interes').textContent = fmtP(Math.round(interes));
  document.getElementById('c-total-seg').textContent = fmtP(Math.round(totalConSeg));
  document.getElementById('calc-box').style.display = 'block';
}

function fmtP(n) { return '$' + Math.round(n).toLocaleString('es-AR'); }
function fmtFecha(d) {
  return d.toLocaleDateString('es-AR', { day: '2-digit', month: '2-digit', year: 'numeric' });
}

function numeroALetras(n) {
  const unidades = ['','UNO','DOS','TRES','CUATRO','CINCO','SEIS','SIETE','OCHO','NUEVE','DIEZ','ONCE','DOCE','TRECE','CATORCE','QUINCE','DIECISEIS','DIECISIETE','DIECIOCHO','DIECINUEVE'];
  const decenas  = ['','DIEZ','VEINTE','TREINTA','CUARENTA','CINCUENTA','SESENTA','SETENTA','OCHENTA','NOVENTA'];
  const centenas = ['','CIENTO','DOSCIENTOS','TRESCIENTOS','CUATROCIENTOS','QUINIENTOS','SEISCIENTOS','SETECIENTOS','OCHOCIENTOS','NOVECIENTOS'];
  if (n === 0) return 'CERO';
  if (n < 0) return 'MENOS ' + numeroALetras(-n);
  let resultado = '';
  if (n >= 1000000) { resultado += numeroALetras(Math.floor(n/1000000)) + (Math.floor(n/1000000)===1?' MILLON ':' MILLONES '); n %= 1000000; }
  if (n >= 1000)    { resultado += (Math.floor(n/1000)===1?'MIL ':numeroALetras(Math.floor(n/1000))+' MIL '); n %= 1000; }
  if (n >= 100)     { resultado += (n===100?'CIEN ':centenas[Math.floor(n/100)]+' '); n %= 100; }
  if (n >= 20)      { resultado += decenas[Math.floor(n/10)] + (n%10!==0?' Y '+unidades[n%10]+' ':' '); }
  else if (n > 0)   { resultado += unidades[n] + ' '; }
  return resultado.trim();
}

function genNumeroCreditio() {
  const d = new Date();
  return `NC-${d.getFullYear()}${String(d.getMonth()+1).padStart(2,'0')}-${String(Math.floor(Math.random()*9000)+1000)}`;
}

window.generar = async function generar() {
  const nombre   = document.getElementById('nombre').value.trim();
  const dni      = document.getElementById('dni').value.trim();
  const tel      = document.getElementById('tel').value.trim();
  const domicilio= document.getElementById('domicilio').value.trim();
  const localidad= document.getElementById('localidad').value.trim();
  const cuit     = document.getElementById('cuit').value.trim();
  const monto    = parseFloat(document.getElementById('monto').value) || 0;
  const contado  = parseFloat(document.getElementById('contado').value) || 0;
  const n        = parseInt(document.getElementById('ncuotas').value) || 0;
  const tasa     = parseFloat(document.getElementById('tasa').value) / 100 || 0;
  const seguro   = parseFloat(document.getElementById('seguro').value) || 0;
  const fecha1Str= document.getElementById('fecha1').value;
  const ncredito = document.getElementById('ncredito').value.trim() || genNumeroCreditio();

  // Familiares
  const fam1 = {
    nombre: document.getElementById('fam1-nombre').value.trim(),
    dni:    document.getElementById('fam1-dni').value.trim(),
    tel:    document.getElementById('fam1-tel').value.trim(),
    dom:    document.getElementById('fam1-dom').value.trim(),
    loc:    document.getElementById('fam1-loc').value.trim(),
    rel:    document.getElementById('fam1-rel').value,
  };
  const fam2 = {
    nombre: document.getElementById('fam2-nombre').value.trim(),
    dni:    document.getElementById('fam2-dni').value.trim(),
    tel:    document.getElementById('fam2-tel').value.trim(),
    dom:    document.getElementById('fam2-dom').value.trim(),
    loc:    document.getElementById('fam2-loc').value.trim(),
    rel:    document.getElementById('fam2-rel').value,
  };

  if (!nombre || !dni || !monto || !n || !tasa) {
    let faltantes = [];
    if(!nombre) faltantes.push('Nombre');
    if(!dni) faltantes.push('DNI');
    if(!monto) faltantes.push('Monto a financiar');
    if(!n || !tasa) faltantes.push('Plan de cuotas (seleccioná un plan o ingresá cuotas y tasa)');
    alert('Faltan completar:\n\n• ' + faltantes.join('\n• '));
    return;
  }

  const cuota = monto * (tasa * Math.pow(1+tasa,n)) / (Math.pow(1+tasa,n)-1);
  const cuotaConSeg = cuota + seguro;
  const total = Math.round(cuota) * n;
  const totalConSeg = Math.round(cuotaConSeg) * n;
  const tea = (Math.pow(1+tasa,12)-1)*100;
  const montoLetras = numeroALetras(Math.round(monto));
  const hoyFmt = fmtFecha(new Date());

  // Generar fechas de cuotas
  const fecha1 = fecha1Str ? new Date(fecha1Str+'T12:00:00') : new Date();
  const cuotas = [];
  for (let i = 0; i < n; i++) {
    const f = new Date(fecha1);
    f.setMonth(f.getMonth() + i);
    cuotas.push({ num: i+1, fecha: fmtFecha(f), monto: Math.round(cuotaConSeg) });
  }

  // Split cuotas en dos columnas
  const mitad = Math.ceil(cuotas.length / 2);
  const col1  = cuotas.slice(0, mitad);
  const col2  = cuotas.slice(mitad);

  const renderCuotasTabla = (lista) => lista.map(c => `
    <tr>
      <td style="text-align:center">${c.num}</td>
      <td>${c.fecha}</td>
    </tr>`).join('');

  const pagareTpl = (tipo) => `
    <div class="pagare">
      <div class="p-header">
        <div class="p-header-left">
          <h2>NICKCEL TECNO &amp; HOGAR S.R.L.</h2>
          <p>CUIT: 30-71899140-0 | San Martin 514, Quitilipi, Chaco</p>
        </div>
        <div class="p-header-right" style="text-align:right">
          <div style="font-size:11px;opacity:.75">Pagaré por: ${fmtP(Math.round(cuotaConSeg)*n)}</div>
        </div>
      </div>

      <div style="display:flex;justify-content:space-between;margin-bottom:10px">
        <div style="font-size:12px"><strong>N° Crédito:</strong> ${ncredito}</div>
        <div style="font-size:12px"><strong>Fecha emisión:</strong> ${hoyFmt}</div>
      </div>

      <div class="p-monto-box">
        <div>
          <div class="p-monto-label">Monto del pagaré</div>
          <div class="p-monto-letras">${montoLetras} PESOS 00/100</div>
        </div>
        <div style="text-align:right">
          <div class="p-monto-val">${fmtP(Math.round(monto))}</div>
          <div style="font-size:10px;color:#666;margin-top:3px">${n} cuotas de <strong style="color:#1e3a5f">${fmtP(Math.round(cuotaConSeg))}</strong>${contado?` | Precio contado: <strong>${fmtP(Math.round(contado))}</strong>`:''}</div>
        </div>
      </div>

      <div class="p-body">
        El día <u>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</u> de <u>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</u> de <u>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</u> Pagaré/emos a
        <strong>NICKCEL TECNO &amp; HOGAR S.R.L.</strong> o a su orden "SIN PROTESTO" (art. 50 Dto. Ley 5965/63) la cantidad de pesos
        <strong><u>${montoLetras}</u></strong> 00/100 por igual valor recibido en efectos a mi/nuestra entera satisfacción.
        Pagadero en Quitilipi, Chaco, República Argentina.
      </div>

      <div class="p-legal">
        En nuestro carácter de libradores dejamos constancia que de conformidad con lo establecido en el art. 36 del Dto. Ley N°5965/63, extendemos el plazo del presente documento hasta dos (2) años de la fecha de emisión. El capital de este pagaré devengará un interés moratorio del <strong>${(tasa*100).toFixed(2)}%</strong> mensual nominal desde la fecha de vencimiento y hasta su efectivo pago. Expresamente el/los firmantes renuncian a la inembargabilidad de los sueldos que prevén las leyes nacionales y provinciales ofreciendo voluntariamente a embargo en todo supuesto de mora o incumplimiento, hasta un máximo del 30% de los mismos. A partir de los 60 días del incumplimiento del plazo fijado para el pago, el deudor se constituirá en MORA de pleno derecho y procederá el cese de la relación contractual de forma automática. El acreedor suspenderá el devengamiento de las cuotas posteriores y estará habilitado a iniciar las acciones tendientes al recupero de la deuda, sin necesidad de notificación al deudor.
        <div style="margin-top:8px;padding-top:8px;border-top:1px solid #ddd;font-size:11px">
          Costo Financiero Total: ${(((Math.round(cuotaConSeg)*n)/monto-1)*100).toFixed(1)}%
          &nbsp;|&nbsp; T.E.A.: ${((Math.pow(1+tasa,12)-1)*100).toFixed(1)}%
        </div>
      </div>

      <div class="p-field-row">
        <div class="p-field"><label>Nombre y Apellido</label><div class="val${nombre?'':' empty'}">${nombre||'_______________________'}</div></div>
        <div class="p-field" style="max-width:140px"><label>DNI</label><div class="val${dni?'':' empty'}">${dni||'____________'}</div></div>
        <div class="p-field" style="max-width:140px"><label>Teléfono ${telVerificado?'<span style="color:#1a7a4a">✓</span>':''}</label><div class="val${tel?'':' empty'}">${tel||'____________'}</div></div>
      </div>
      <div class="p-field-row" style="margin-top:6px">
        <div class="p-field"><label>Domicilio</label><div class="val${domicilio?'':' empty'}">${domicilio||'_______________________'}</div></div>
        <div class="p-field"><label>Localidad</label><div class="val${localidad?'':' empty'}">${localidad||'____________'}</div></div>
        <div class="p-field" style="max-width:180px"><label>CUIT</label><div class="val${cuit?'':' empty'}">${cuit||'____________'}</div></div>
      </div>

      ${(fam1.nombre||fam2.nombre)?`
      <div style="background:#f5f8fc;border-radius:4px;padding:8px 10px;margin-top:10px">
        <div style="font-size:10px;font-weight:700;color:#2e75b6;text-transform:uppercase;letter-spacing:.05em;margin-bottom:6px">Referencias familiares</div>
        ${fam1.nombre?`
        <div style="display:flex;gap:12px;font-size:11px;margin-bottom:4px;flex-wrap:wrap">
          <span><strong>${fam1.rel}:</strong> ${fam1.nombre}</span>
          <span>DNI: ${fam1.dni||'—'}</span>
          <span>Tel: ${fam1.tel||'—'}</span>
          <span>${fam1.dom||''}${fam1.loc?' — '+fam1.loc:''}</span>
        </div>`:''}
        ${fam2.nombre?`
        <div style="display:flex;gap:12px;font-size:11px;flex-wrap:wrap">
          <span><strong>${fam2.rel}:</strong> ${fam2.nombre}</span>
          <span>DNI: ${fam2.dni||'—'}</span>
          <span>Tel: ${fam2.tel||'—'}</span>
          <span>${fam2.dom||''}${fam2.loc?' — '+fam2.loc:''}</span>
        </div>`:''}
      </div>`:''}

      <div class="p-firmas">
        <div class="p-firma-box">
          <div style="height:50px"></div>
          <div class="p-firma-line">Firma y aclaración del titular<br><small>Nombre: ${nombre} | DNI: ${dni}</small></div>
        </div>
        <div class="p-firma-box">
          <div style="height:50px"></div>
          <div class="p-firma-line">Firma y aclaración del co-titular (si aplica)<br><small>Nombre: _________________ | DNI: _________</small></div>
        </div>
      </div>
    </div>`;

  const planCuotasHtml = `
    <div class="cuotas-wrap">
      <div class="c-header">
        <h3>COMPROBANTE DE CUOTAS — CLIENTE</h3>
        <div style="font-size:11px;opacity:.8">NICKCEL TECNO &amp; HOGAR S.R.L. | San Martin 514, Quitilipi, Chaco | WhatsApp: 3644924970</div>
        <span style="font-size:12px">N° Crédito: ${ncredito}</span>
      </div>

      <div class="c-cliente-info">
        <div class="c-info-item"><label>Cliente</label><div class="val">${nombre}</div></div>
        <div class="c-info-item"><label>DNI</label><div class="val">${dni}</div></div>
        <div class="c-info-item"><label>Teléfono</label><div class="val">${tel||'—'}</div></div>
        <div class="c-info-item"><label>Monto crédito</label><div class="val">${fmtP(Math.round(monto))}</div></div>
        <div class="c-info-item"><label>Cant. cuotas</label><div class="val">${n} cuotas</div></div>
        <div class="c-info-item"><label>Tasa mensual</label><div class="val">${(tasa*100).toFixed(2)}% | T.E.A. ${tea.toFixed(1)}%</div></div>
      </div>

      <div class="cuotas-grid">
        <table class="cuotas-table">
          <thead><tr><th>N°</th><th>Vencimiento</th></tr></thead>
          <tbody>${renderCuotasTabla(col1)}</tbody>
        </table>
        <table class="cuotas-table">
          <thead><tr><th>N°</th><th>Vencimiento</th></tr></thead>
          <tbody>${col2.length ? renderCuotasTabla(col2) : '<tr><td colspan="2" style="text-align:center;color:#aaa;padding:20px">—</td></tr>'}</tbody>
        </table>
      </div>

      <div class="resumen-caja">
        <div class="res-row"><span>Precio de contado</span><span>${contado?fmtP(contado):'—'}</span></div>
        <div class="res-row"><span>Monto financiado</span><span>${fmtP(Math.round(monto))}</span></div>
        <div class="res-row"><span>Cuota mensual</span><span>${fmtP(Math.round(cuota))}</span></div>
        ${seguro>0?`<div class="res-row"><span>Seguro de vida / cuota</span><span>${fmtP(seguro)}</span></div>`:''}
        ${seguro>0?`<div class="res-row"><span>Cuota total con seguro</span><span>${fmtP(Math.round(cuotaConSeg))}</span></div>`:''}
        <div class="res-row"><span>COSTO FINANCIERO TOTAL</span><span>${(((totalConSeg/monto)-1)*100).toFixed(1)}%</span></div>
      </div>

      <div style="margin-top:16px;display:grid;grid-template-columns:1fr 1fr;gap:20px">
        <div style="text-align:center">
          <div style="height:40px;border-bottom:1px solid #333"></div>
          <div style="font-size:11px;color:#555;margin-top:4px">Firma titular — ${nombre}</div>
        </div>
        <div style="text-align:center">
          <div style="height:40px;border-bottom:1px solid #333"></div>
          <div style="font-size:11px;color:#555;margin-top:4px">Firma representante — NICKCEL S.R.L.</div>
        </div>
      </div>
    </div>`;

  document.getElementById('preview-content').innerHTML =
    `<div class="pagare-wrap">
      ${pagareTpl('COMERCIO')}
    </div>
    ${planCuotasHtml}`;

  document.getElementById('prev-title').textContent = `Pagaré generado — ${nombre} | ${fmtP(Math.round(monto))} en ${n} cuotas`;

  // GUARDAR EN CARTERA
  await guardarCredito({
    ncredito, nombre, dni, tel, domicilio, localidad, cuit,
    monto: Math.round(monto),
    contado: Math.round(contado)||0,
    cuotaMonto: Math.round(cuotaConSeg),
    nCuotas: n,
    tasa: tasa*100,
    fechaEmision: hoyFmt,
    fam1, fam2,
    cuotas: cuotas.map(c=>({
      num: c.num,
      fecha: c.fecha,
      fechaISO: new Date(fecha1.getFullYear(), fecha1.getMonth()+c.num-1, fecha1.getDate()).toISOString().split('T')[0],
      monto: c.monto,
      pagada: false,
      fechaPago: null
    }))
  });
}

window.limpiar = function() {
  ['nombre','dni','tel','domicilio','localidad','cuit','monto','contado','ncuotas','tasa','seguro','ncredito',
   'fam1-nombre','fam1-dni','fam1-tel','fam1-dom','fam1-loc',
   'fam2-nombre','fam2-dni','fam2-tel','fam2-dom','fam2-loc'].forEach(id => {
    document.getElementById(id).value = '';
  });
  planActivo = null;
  document.querySelectorAll('.tb').forEach(b => b.classList.remove('active'));
  document.getElementById('calc-box').style.display = 'none';
  document.getElementById('preview-content').innerHTML = '<div style="text-align:center;padding:60px 20px;color:#999;font-size:14px">Complete los datos del cliente y el monto para generar el pagaré</div>';
  document.getElementById('prev-title').textContent = 'Complete los datos y presione "Generar Pagaré"';
  document.getElementById('fecha1').value = new Date().toISOString().split('T')[0];
  codigoActual = null; telVerificado = false;
  document.getElementById('verify-box').style.display='none';
  document.getElementById('tel-status').innerHTML='';
  showTab('cliente', document.getElementById('tab-btn-cliente'));
}
</script>

<script>
// ============================================
// LOGIN Y ROLES
// ============================================
const PASS_ADMIN = '5706';
const PASS_VENDEDOR = '1234';
let rolActual = null; // 'admin' o 'vendedor'

window.doLogin = function() {
  const pass = document.getElementById('inp-login-pass').value;
  const err = document.getElementById('login-err');
  if(pass === PASS_ADMIN) {
    rolActual = 'admin';
  } else if(pass === PASS_VENDEDOR) {
    rolActual = 'vendedor';
  } else {
    err.textContent = 'Contraseña incorrecta.';
    return;
  }
  document.getElementById('login-screen').style.display = 'none';
  document.getElementById('main-app').style.display = 'block';
  document.getElementById('rol-indicator').textContent = rolActual === 'admin' ? '👑 Admin' : '👤 Vendedor';
  aplicarPermisos();
}

window.doLogout = function() {
  rolActual = null;
  document.getElementById('main-app').style.display = 'none';
  document.getElementById('login-screen').style.display = 'flex';
  document.getElementById('inp-login-pass').value = '';
  document.getElementById('login-err').textContent = '';
}

function aplicarPermisos() {
  // No hay nada que ocultar en la pantalla de pagaré
  // Los permisos se aplican dinámicamente en renderCartera
}

// Parchar renderCartera para aplicar permisos de rol
const _renderCarteraOrig = window.renderCartera || null;

// Override de eliminarCredito para vendedores
const _eliminarCreditoOrig = window.eliminarCredito;
window.eliminarCredito = async function(ncredito) {
  if(rolActual !== 'admin') {
    alert('Solo el administrador puede eliminar créditos.');
    return;
  }
  if(_eliminarCreditoOrig) await _eliminarCreditoOrig(ncredito);
}

// Override de anularCuota — solo admin
window.anularCuota = async function(ncredito, qi) {
  if(rolActual !== 'admin') {
    alert('Solo el administrador puede anular pagos.');
    return;
  }
  if(!confirm('¿Anular este pago? La cuota volverá a estado pendiente.')) return;

  // Importar las funciones de Firebase desde el módulo ya cargado
  const cred = window._carteraCache ? window._carteraCache.find(c=>c.ncredito===ncredito) : null;
  if(!cred) { alert('No se encontró el crédito.'); return; }

  cred.cuotas[qi].pagada = false;
  cred.cuotas[qi].fechaPago = null;

  try {
    // Usar el updateDoc global expuesto por el módulo
    await window._updateCuotas(ncredito, cred.cuotas);
    window._renderCarteraFn && window._renderCarteraFn(window._filtroActual || 'todos');
    alert('Pago anulado correctamente. La cuota volvió a estado pendiente.');
  } catch(e) {
    alert('Error al anular. Verificá tu conexión.');
  }
}
</script>

</div><!-- /main-app -->
</body>
</html>
