# Psi_Chat
Aplicativo de Acolhimento
{
  "Sigmund Freud": "A ansiedade pode estar ligada a conflitos inconscientes.",
  "Carl Jung": "A ansiedade pode ser um chamado do inconsciente para individuação.",
  "B.F. Skinner": "A ansiedade pode ser reforçada por estímulos ambientais.",
  "Carl Rogers": "Um ambiente de aceitação incondicional pode ajudar na ansiedade.",
  "Lev Vygotsky": "A interação social pode ajudar a reorganizar o pensamento ansioso."
}
<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chat Psicológico</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; }
        .chat-box { width: 50%; margin: auto; border: 1px solid black; padding: 20px; }
        .mensagem { text-align: left; margin: 10px; }
        .usuario { color: blue; }
        .bot { color: green; }
    </style>
</head>
<body>
    <h2>Converse com Psicólogos Famosos</h2>
    <div class="chat-box" id="chat-box"></div>
    <select id="psicologo">
        <option value="Sigmund Freud">Sigmund Freud</option>
        <option value="Carl Jung">Carl Jung</option>
        <option value="B.F. Skinner">B.F. Skinner</option>
        <option value="Carl Rogers">Carl Rogers</option>
        <option value="Lev Vygotsky">Lev Vygotsky</option>
    </select>
    <input type="text" id="pergunta" placeholder="Digite sua pergunta">
    <button onclick="enviarPergunta()">Enviar</button>

    <script>
        async function enviarPergunta() {
            let psicologo = document.getElementById("psicologo").value;
            let pergunta = document.getElementById("pergunta").value;
            let chatBox = document.getElementById("chat-box");

            chatBox.innerHTML += `<p class="mensagem usuario"><strong>Você:</strong> ${pergunta}</p>`;

            try {
                let response = await fetch('dados.json');
                let data = await response.json();
                let resposta = data[psicologo] || "Não tenho uma resposta para isso.";
                
                chatBox.innerHTML += `<p class="mensagem bot"><strong>${psicologo}:</strong> ${resposta}</p>`;
            } catch (error) {
                chatBox.innerHTML += `<p class="mensagem bot"><strong>Erro:</strong> Não consegui acessar as respostas.</p>`;
            }

            document.getElementById("pergunta").value = "";
        }
    </script>
</body>
</html>
