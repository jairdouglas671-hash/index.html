# index.html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FechaOrçamento</title>

<style>
body {
  font-family: Arial, sans-serif;
  background: #f1f3f5;
  margin: 0;
  padding: 20px;
}

.container {
  max-width: 500px;
  margin: auto;
  background: white;
  padding: 22px;
  border-radius: 12px;
}

h1 {
  text-align: center;
  color: #155eef;
}

input {
  width: 100%;
  padding: 12px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 6px;
}

button {
  width: 100%;
  padding: 14px;
  margin-top: 12px;
  background: #155eef;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 16px;
}

#resultado {
  margin-top: 20px;
  padding: 15px;
  background: #eef4ff;
  border-radius: 8px;
}
</style>
</head>

<body>

<div class="container">

<h1>FechaOrçamento</h1>
<p>Crie seu orçamento profissional.</p>

<input id="prestador" placeholder="Nome do prestador">

<input id="cliente" placeholder="Nome do cliente">

<input id="servico" placeholder="Descrição do serviço">

<input id="quantidade" type="number"
placeholder="Quantidade" min="1" step="1">

<input id="preco" type="number"
placeholder="Preço por unidade (R$)" min="0" step="0.01">

<button onclick="gerarOrcamento()">
Gerar orçamento
</button>

<div id="resultado"></div>

</div>

<script>
function gerarOrcamento() {

const prestador = document.getElementById("prestador").value;
const cliente = document.getElementById("cliente").value;
const servico = document.getElementById("servico").value;
const quantidade = Number(document.getElementById("quantidade").value);
const preco = Number(document.getElementById("preco").value);

if (!prestador || !cliente || !servico ||
quantidade <= 0 || preco < 0 ||
!Number.isFinite(quantidade) ||
!Number.isFinite(preco)) {
alert("Preencha todos os campos corretamente.");
return;
}

const total = quantidade * preco;

document.getElementById("resultado").innerHTML = `
<h2>Orçamento</h2>
<p><b>Prestador:</b> ${escapar(prestador)}</p>
<p><b>Cliente:</b> ${escapar(cliente)}</p>
<p><b>Serviço:</b> ${escapar(servico)}</p>
<p><b>Quantidade:</b> ${quantidade}</p>
<p><b>Valor unitário:</b> ${formatar(preco)}</p>
<h2>Total: ${formatar(total)}</h2>
<button onclick="window.print()">Imprimir / Salvar PDF</button>
`;
}

function formatar(valor) {
return valor.toLocaleString("pt-BR", {
style: "currency",
currency: "BRL"
});
}

function escapar(texto) {
return texto.replace(/[&<>"']/g, function(c) {
return {
"&": "&amp;",
"<": "&lt;",
">": "&gt;",
'"': "&quot;",
"'": "&#39;"
}[c];
});
}
</script>

</body>
</html>
