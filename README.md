# Trabalho-F-bio
Trabalho Fabão 
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meu Arquivo QR</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <style>
        * {
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }
        body {
            background: #f0f2f5;
            max-width: 400px;
            margin: 30px auto;
            padding: 20px;
        }
        .container {
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        h2 {
            text-align: center;
            color: #1a73e8;
            margin-top: 0;
        }
        input {
            width: 100%;
            padding: 12px;
            margin: 8px 0;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
        }
        button {
            width: 100%;
            padding: 12px;
            background: #1a73e8;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            cursor: pointer;
            margin-top: 10px;
        }
        button:hover {
            background: #1557b0;
        }
        #qrcode {
            text-align: center;
            margin-top: 20px;
        }
        #downloadBtn {
            background: #34a853;
            margin-top: 15px;
        }
        #downloadBtn:hover {
            background: #28863f;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>📁 Arquivar com QR</h2>

    <label>🔗 Link do Arquivo (Google Drive, etc):</label>
    <input type="text" id="linkInput" placeholder="Cole o link aqui...">

    <label>📝 Nome do Arquivo:</label>
    <input type="text" id="nomeInput" placeholder="Ex: Contrato.pdf">

    <button onclick="gerarQR()">Gerar QR Code</button>

    <div id="qrcode"></div>
    <button id="downloadBtn" style="display:none;" onclick="baixarQR()">⬇️ Baixar QR Code</button>
</div>

<script>
let qrCode;

function gerarQR() {
    const link = document.getElementById("linkInput").value;
    const nome = document.getElementById("nomeInput").value;

    if (!link) {
        alert("Cole o link primeiro!");
        return;
    }

    document.getElementById("qrcode").innerHTML = "";
    
    qrCode = new QRCode(document.getElementById("qrcode"), {
        text: link,
        width: 256,
        height: 256,
        colorDark : "#000000",
        colorLight : "#ffffff",
        correctLevel : QRCode.CorrectLevel.H
    });

    document.getElementById("downloadBtn").style.display = "block";
}

function baixarQR() {
    const img = document.querySelector("#qrcode img");
    const nomeArquivo = document.getElementById("nomeInput").value || "qrcode";
    
    const canvas = document.createElement("canvas");
    canvas.width = img.width;
    canvas.height = img.height;
    const ctx = canvas.getContext("2d");
    ctx.drawImage(img, 0, 0);
    
    const a = document.createElement("a");
    a.download = `QR_${nomeArquivo}.png`;
    a.href = canvas.toDataURL("image/png");
    a.click();
}
</script>

</body>
</html>
