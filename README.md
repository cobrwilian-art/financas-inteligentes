<!DOCTYPE html><html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Finanças Inteligentes | Wilian Alves</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Poppins',sans-serif}
body{background:#0f172a;color:#e2e8f0}
header{background:linear-gradient(135deg,#0f172a,#1e293b);padding:80px 20px;text-align:center}
h1{font-size:2.8rem}
.container{max-width:1100px;margin:auto;padding:60px 20px}
.btn{display:inline-block;margin-top:20px;padding:14px 30px;background:#22c55e;color:#fff;text-decoration:none;border-radius:40px;font-weight:600;transition:.3s}
.btn:hover{background:#16a34a}
.section-title{font-size:2rem;margin-bottom:30px;text-align:center}
.card{background:#1e293b;padding:30px;border-radius:20px;margin-bottom:30px;box-shadow:0 10px 30px rgba(0,0,0,.3)}
input,textarea,select{width:100%;padding:12px;margin-top:10px;border-radius:10px;border:none}
button{padding:12px 20px;border:none;border-radius:30px;background:#22c55e;color:white;font-weight:600;cursor:pointer;margin-top:15px}
button:hover{background:#16a34a}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:20px}
.blog-post{background:#0f172a;padding:20px;border-radius:15px}
footer{text-align:center;padding:40px;background:#020617;margin-top:40px}
.premium-badge{background:#22c55e;color:#000;padding:5px 15px;border-radius:20px;font-size:.8rem;font-weight:700;display:inline-block;margin-bottom:15px}
</style>
</head>
<body><header>
<div class="premium-badge">Autoridade em Educação Financeira</div>
<h1>Domine Suas Finanças e Construa Liberdade Financeira</h1>
<p>Aprenda a organizar, investir e criar novas fontes de renda.</p>
<a href="#ebook" class="btn">Baixar eBook Gratuito</a>
</header><div class="container" id="ebook">
<h2 class="section-title">Baixe o eBook Gratuito</h2>
<div class="card">
<p>Guia Prático para Organizar Sua Vida Financeira e Começar a Investir do Zero.</p>
<input type="text" placeholder="Seu nome">
<input type="email" placeholder="Seu melhor e-mail">
<button>Quero Receber Agora</button>
</div>
</div><div class="container">
<h2 class="section-title">Calculadora Financeira</h2>
<div class="card">
<label>Valor Investido (R$)</label>
<input type="number" id="valor">
<label>Taxa de Juros Mensal (%)</label>
<input type="number" id="taxa">
<label>Meses</label>
<input type="number" id="meses">
<button onclick="calcular()">Calcular</button>
<h3 id="resultado"></h3>
</div>
</div><div class="container">
<h2 class="section-title">Simulação de Renda Extra</h2>
<div class="card">
<label>Valor extra por dia (R$)</label>
<input type="number" id="extraDia">
<button onclick="simularRenda()">Simular</button>
<h3 id="resultadoRenda"></h3>
<canvas id="grafico"></canvas>
</div>
</div><div class="container">
<h2 class="section-title">Blog</h2>
<div class="grid">
<div class="blog-post">
<h3>Como sair das dívidas mais rápido</h3>
<p>Estratégias práticas para eliminar dívidas e recuperar sua saúde financeira.</p>
</div>
<div class="blog-post">
<h3>Primeiros passos nos investimentos</h3>
<p>Aprenda onde investir mesmo começando com pouco dinheiro.</p>
</div>
<div class="blog-post">
<h3>Ideias de renda extra em 2026</h3>
<p>Descubra formas modernas de aumentar seus ganhos.</p>
</div>
</div>
</div><footer>
<p>© 2026 Wilian Alves | Finanças Inteligentes</p>
</footer><script>
function calcular(){
let valor=parseFloat(document.getElementById('valor').value);
let taxa=parseFloat(document.getElementById('taxa').value)/100;
let meses=parseInt(document.getElementById('meses').value);
let montante=valor*Math.pow((1+taxa),meses);
document.getElementById('resultado').innerText='Montante final: R$ '+montante.toFixed(2);
}

function simularRenda(){
let valor=parseFloat(document.getElementById('extraDia').value);
let mensal=valor*30;
let anual=mensal*12;
document.getElementById('resultadoRenda').innerText='Renda mensal: R$ '+mensal.toFixed(2)+' | Renda anual: R$ '+anual.toFixed(2);

new Chart(document.getElementById('grafico'),{
type:'bar',
data:{
labels:['Mensal','Anual'],
datasets:[{label:'Projeção de Renda',data:[mensal,anual]}]
}
});
}
</script></body>
</html>
