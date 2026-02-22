# OPENAI_API_KEY<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>TTS Android</title>
<style>
body{
background:#111;
color:white;
font-family:Arial;
text-align:center;
padding:20px;
}
textarea{
width:90%;
height:120px;
}
button{
padding:12px;
margin-top:15px;
}
select{
padding:10px;
margin-top:10px;
}
</style>
</head>
<body>

<h2>Texto para Fala</h2>

<textarea id="text">Teste de voz funcionando</textarea>
<br>

<select id="voices"></select>
<br>

<button onclick="falar()">Gerar Voz</button>

<script>
let synth = window.speechSynthesis;
let voiceSelect = document.getElementById("voices");

function loadVoices() {
  let voices = synth.getVoices();
  voiceSelect.innerHTML = "";
  voices.forEach((voice, i) => {
    let option = document.createElement("option");
    option.value = i;
    option.textContent = voice.name + " - " + voice.lang;
    voiceSelect.appendChild(option);
  });
}

speechSynthesis.onvoiceschanged = loadVoices;

function falar() {
  synth.cancel(); // limpa fila anterior
  let texto = document.getElementById("text").value;
  let utterance = new SpeechSynthesisUtterance(texto);
  let voices = synth.getVoices();
  utterance.voice = voices[voiceSelect.value];
  utterance.lang = "pt-BR";
  utterance.rate = 1;
  utterance.pitch = 1;
  synth.speak(utterance);
}
</script>

</body>
</html>
