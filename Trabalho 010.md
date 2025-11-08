<!DOCTYPE html>
<html>
<head>
    <meta charset='utf-8'>
    <meta http-equiv='X-UA-Compatible' content='IE=edge'>
    <title>Trabalho 010</title>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      transition: background-color 0.5s;
    }

    table {
      margin: 50px auto;
      border-collapse: collapse;
      border: 2px solid #333;
      background-color: #fff8dc;
      border-radius: 12px;
      box-shadow: 0 0 10px rgba(0,0,0,0.2);
    }

    td {
      padding: 15px;
    }

    input, select, button {
      padding: 8px;
      margin: 5px;
      border-radius: 6px;
      border: 1px solid #333;
      font-size: 14px;
    }

    #resultado {
      font-weight: bold;
      font-size: 1.2em;
      margin-top: 20px;
    }

    footer {
      margin-top: 30px;
      font-size: 0.9em;
    }
  </style>
</head>
<body>
  <h1>Conversor de Temperaturas</h1>

  <table>
    <tr>
      <td>Valor:</td>
      <td><input type="number" id="valor" placeholder="Insere a temperatura" oninput="validarValor()"></td>
    </tr>
    <tr>
      <td>De:</td>
      <td>
        <select id="de">
          <option value="C">Celsius</option>
          <option value="F">Fahrenheit</option>
          <option value="K">Kelvin</option>
        </select>
      </td>
    </tr>
    <tr>
      <td>Para:</td>
      <td>
        <select id="para">
          <option value="C">Celsius</option>
          <option value="F">Fahrenheit</option>
          <option value="K">Kelvin</option>
        </select>
      </td>
    </tr>
    <tr>
      <td colspan="2">
        <button onclick="converter()">Converter</button>
        <button onclick="usarPrompt()">Usar Prompt</button>
      </td>
    </tr>
  </table>

  <div id="resultado"></div>

  <script>
    function validarValor() {
      const valor = document.getElementById("valor").value;
      if (isNaN(valor)) {
        alert("Por favor, insere um número válido!");
        document.getElementById("valor").value = "";
      }
    }

    function converter() {
      const valor = parseFloat(document.getElementById("valor").value);
      const de = document.getElementById("de").value;
      const para = document.getElementById("para").value;

      if (isNaN(valor)) {
        alert("Insere um valor antes de converter!");
        return;
      }

      let resultado = 0;

      // Conversões
      if (de === para) resultado = valor;
      else if (de === "C" && para === "F") resultado = valor * 9/5 + 32;
      else if (de === "F" && para === "C") resultado = (valor - 32) * 5/9;
      else if (de === "C" && para === "K") resultado = valor + 273.15;
      else if (de === "K" && para === "C") resultado = valor - 273.15;
      else if (de === "F" && para === "K") resultado = (valor - 32) * 5/9 + 273.15;
      else if (de === "K" && para === "F") resultado = (valor - 273.15) * 9/5 + 32;

      resultado = resultado.toFixed(2);

      document.getElementById("resultado").innerHTML = 
        `Resultado: ${resultado} °${para}`;

      mudarCorDeFundo(para, resultado);
    }

    function mudarCorDeFundo(escala, valor) {
      let tempCelsius;

      // Converter tudo para Celsius para comparar
      if (escala === "C") tempCelsius = valor;
      else if (escala === "F") tempCelsius = (valor - 32) * 5/9;
      else if (escala === "K") tempCelsius = valor - 273.15;

      if (tempCelsius <= 10) document.body.style.backgroundColor = "lightblue";
      else if (tempCelsius >= 25) document.body.style.backgroundColor = "red";
      else document.body.style.backgroundColor = "yellow";
    }

    function usarPrompt() {
      const valor = parseFloat(prompt("Insere o valor da temperatura:"));
      if (isNaN(valor)) {
        alert("Valor inválido!");
        return;
      }
      document.getElementById("valor").value = valor;
      converter();
    }
  </script>
  <footer>
    <p>Fórmulas baseadas em: 
      <a href="https://www.rapidtables.com/convert/temperature/index.html" target="_blank">
        RapidTables - Conversões de Temperatura
      </a>
    </p>
  </footer>
</body>
</html>
