<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Calculadora Bioelétrica v2.0 - Ordem Paranormal</title>
  <style>
    * { box-sizing: border-box; }
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #0d0d10;
      color: #e1e1e6;
      padding: 16px;
      margin: 0;
      display: flex;
      justify-content: center;
    }
    .card {
      background-color: #191920;
      border: 2px solid #996dff;
      border-radius: 16px;
      padding: 24px;
      max-width: 480px;
      width: 100%;
      box-shadow: 0 0 25px rgba(153, 109, 255, 0.25);
    }
    h1 {
      text-align: center;
      color: #996dff;
      margin-top: 0;
      margin-bottom: 6px;
      font-size: 24px;
      letter-spacing: 1px;
    }
    .subtitle {
      text-align: center;
      color: #7c7c8a;
      font-size: 13px;
      margin-bottom: 20px;
    }
    label {
      font-size: 14px;
      font-weight: bold;
      color: #00b37e;
      display: block;
      margin-bottom: 6px;
    }
    input[type="number"] {
      width: 100%;
      padding: 14px;
      margin-bottom: 20px;
      border-radius: 8px;
      border: 2px solid #323238;
      background-color: #0d0d10;
      color: #fff;
      font-size: 22px;
      font-weight: bold;
      text-align: center;
      outline: none;
      transition: border-color 0.2s;
    }
    input[type="number"]:focus {
      border-color: #996dff;
    }
    .res-box {
      background-color: #202028;
      border-left: 4px solid #996dff;
      border-radius: 8px;
      padding: 14px;
      margin-bottom: 12px;
    }
    .res-box.defesa { border-left-color: #00b37e; }
    .res-box.cura { border-left-color: #f75a68; }
    .res-box.mobi { border-left-color: #fba94c; }

    .res-title {
      font-size: 12px;
      color: #a8a8b3;
      text-transform: uppercase;
      font-weight: bold;
      letter-spacing: 0.8px;
    }
    .res-value {
      font-size: 20px;
      font-weight: bold;
      color: #fff;
      margin-top: 4px;
    }
    .sub-info {
      font-size: 13px;
      color: #8d8d99;
      margin-top: 4px;
      line-height: 1.4;
    }
    .warning {
      font-size: 12px;
      color: #fba94c;
      background-color: rgba(251, 169, 76, 0.1);
      padding: 8px;
      border-radius: 6px;
      margin-top: 8px;
      border-left: 3px solid #fba94c;
    }
  </style>
</head>
<body>

<div class="card">
  <h1>⚡ CALCULADORA BIOELÉTRICA</h1>
  <div class="subtitle">Sistema Personalizado • Ordem Paranormal v2.0</div>
  
  <label for="peInput">INFORME A QUANTIDADE DE PE (CARGA):</label>
  <input type="number" id="peInput" placeholder="Ex: 14" oninput="calcular()" min="1">

  <!-- DANO DE ATAQUE -->
  <div class="res-box">
    <div class="res-title">💥 Potência de Ataque</div>
    <div class="res-value" id="danoRes">+0d6</div>
    <div class="sub-info" id="danoMedio">Dano Médio Estimado: 0</div>
    <div class="warning" id="estAviso">⚠️ Exige reforço igual na Estrutura do Braço para evitar dano recíproco.</div>
  </div>

  <!-- DEFESA & RESISTÊNCIA -->
  <div class="res-box defesa">
    <div class="res-title">🛡️ Armadura & Resistência Bioelétrica</div>
    <div class="res-value" id="defRes">RD 0 | Defesa: +0</div>
    <div class="sub-info" id="defDetalhe">Absorve dano físico/elemental e aumenta reflexos d20.</div>
  </div>

  <!-- CURA PRÓPRIA -->
  <div class="res-box cura">
    <div class="res-title">🩸 Regeneração Celular (Mitose em Si)</div>
    <div class="res-value" id="curaRes">0 PV Restaurados</div>
    <div class="sub-info" id="curaMembro">Status Celular: Cortes e escoriações leves.</div>
  </div>

  <!-- CURA ALIADO -->
  <div class="res-box cura">
    <div class="res-title">⚡ Eletro-Cauterização em Aliados</div>
    <div class="res-value" id="aliadoRes">0 PV Restaurados</div>
    <div class="sub-info" id="aliadoObs">Arco elétrico de toque para fechar feridas.</div>
  </div>

  <!-- MOBILIDADE -->
  <div class="res-box mobi">
    <div class="res-title">🏃 Mobilidade & Impulso das Pernas</div>
    <div class="res-value" id="mobiRes">+0m Deslocamento</div>
    <div class="sub-info" id="mobiSalto">Capacidade de Salto Vertical: 0 metros.</div>
  </div>
</div>

<script>
function calcular() {
  let pe = parseFloat(document.getElementById('peInput').value);

  if (isNaN(pe) || pe <= 0) {
    document.getElementById('danoRes').innerText = "+0d6 de Energia";
    document.getElementById('danoMedio').innerText = "Dano Médio Estimado: 0";
    document.getElementById('estAviso').innerText = "⚠️ Exige reforço igual na Estrutura do Braço para evitar dano recíproco.";
    document.getElementById('defRes').innerText = "RD 0 | Defesa: +0";
    document.getElementById('curaRes').innerText = "0 PV Restaurados";
    document.getElementById('curaMembro').innerText = "Status Celular: Sem ativação.";
    document.getElementById('aliadoRes').innerText = "0 PV Restaurados";
    document.getElementById('aliadoObs').innerText = "Arco elétrico de toque para fechar feridas.";
    document.getElementById('mobiRes').innerText = "+0m Deslocamento";
    document.getElementById('mobiSalto').innerText = "Capacidade de Salto Vertical: 0 metros.";
    return;
  }

  // 1. DANO DE ATAQUE: d6 = PE^1.25
  let dados = Math.floor(Math.pow(pe, 1.25));
  let danoMedio = Math.round(dados * 3.5);
  document.getElementById('danoRes').innerText = `+${dados}d6 de Energia`;
  document.getElementById('danoMedio').innerText = `Dano Médio Estimado: ~${danoMedio} de dano`;
  document.getElementById('estAviso').innerHTML = `⚠️ <b>Estrutura do Braço:</b> Requer <b>${pe} PE</b> dedicados em reforço físico para não sofrer fraturas/dano no próprio corpo.`;

  // 2. DEFESA E RESISTÊNCIA: RD = PE * 1.1 | Defesa = sqrt(PE) * 2.5
  let rd = Math.floor(pe * 1.1);
  let bonusDef = Math.floor(Math.sqrt(pe) * 2.5);
  document.getElementById('defRes').innerText = `RD ${rd} | Defesa: +${bonusDef}`;

  // 3. CURA PRÓPRIA: PV = PE^1.6 + 1
  let curaPV = Math.floor(Math.pow(pe, 1.6) + 1);
  document.getElementById('curaRes').innerText = `${curaPV} PV Restaurados`;

  let statusRegen = "Estanca sangramentos e regenera tecidos musculares.";
  if (pe >= 21 && pe < 26) statusRegen = "🧬 <b>Regeneração Extrema:</b> Recria dedos/articulações amputadas.";
  else if (pe >= 26 && pe < 30) statusRegen = "🧬 <b>Regeneração Extrema:</b> Recria mão ou pé completo amputado.";
  else if (pe >= 30 && pe < 50) statusRegen = "🦾 <b>Regeneração Titânica:</b> Recria braço ou perna inteira do zero!";
  else if (pe >= 50) statusRegen = "⚡ <b>Ressurgimento Mitótico:</b> Reconstituição celular instantânea de órgãos vitais destruídos!";
  document.getElementById('curaMembro').innerHTML = statusRegen;

  // 4. CURA ALIADO (MÁX 13 PE)
  if (pe > 13) {
    document.getElementById('aliadoRes').innerText = "⚠️ Limite Excedido";
    document.getElementById('aliadoObs').innerText = "O corpo do aliado não possui a mutação celular. Aplicar mais de 13 PE causa queimaduras elétricas severas (Máximo permitido: 13 PE = 13 PV).";
  } else {
    document.getElementById('aliadoRes').innerText = `${Math.floor(pe)} PV Restaurados`;
    let obsAliado = "Cauterização rústica de feridas abertas.";
    if (pe === 6) obsAliado = "⚡ <b>Modo Desfibrilação:</b> Reanima aliado no estado Moribundo com 1 PV!";
    document.getElementById('aliadoObs').innerHTML = obsAliado;
  }

  // 5. MOBILIDADE: Deslocamento = +1.5m por PE | Salto = +0.75m por PE
  let deslo = (pe * 1.5).toFixed(1);
  let salto = (pe * 0.75).toFixed(1);
  document.getElementById('mobiRes').innerText = `+${deslo}m de Deslocamento`;
  document.getElementById('mobiSalto').innerText = `Capacidade de Salto Vertical: +${salto}m de altura.`;
}
</script>

</body>
</html>
