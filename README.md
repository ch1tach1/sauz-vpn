<!DOCTYPE html>
<html lang="ru">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Sauz VPN</title>
    <style>
      html,
      body {
        margin: 0;
        padding: 0;
        height: 100%;
        background: black;
        font-family: "Arial", sans-serif;
        color: #e0e0e0;
        display: flex;
        align-items: center;
        justify-content: center;
      }

      .container {
        background: rgba(0, 0, 0, 0.6);
        padding: 30px;
        border-radius: 15px;
        max-width: 600px;
        width: 90%;
        text-align: center;
        box-shadow: 0 0 25px rgba(255, 60, 60, 0.6);
      }

      h1 {
        font-size: 26px;
        margin-bottom: 20px;
        color: #ff3c3c;
        text-shadow: 0 0 8px #ff3c3c, 0 0 12px #ff1c1c;
      }

      pre {
        white-space: pre-wrap;
        word-break: break-word;
        background: rgba(255, 255, 255, 0.05);
        padding: 20px;
        border-radius: 10px;
        overflow-x: auto;
        font-size: 14px;
      }

      button {
        margin-top: 15px;
        padding: 10px 20px;
        font-size: 16px;
        background: #ff3c3c;
        color: white;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        box-shadow: 0 0 8px #ff3c3c;
        display: none;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <h1>Sauz VPN</h1>
      <pre id="output">Загрузка...</pre>
      <button id="openBtn">Открыть приложение</button>
    </div>

    <script>
      function decodeVMess(vmessURL) {
        try {
          const base64Payload = vmessURL.split("vmess://")[1];
          const jsonString = atob(base64Payload);
          const data = JSON.parse(jsonString);
          return JSON.stringify(data, null, 2);
        } catch (e) {
          return "Ошибка декодирования VMess ссылки";
        }
      }

      function getParam(name) {
        const urlParams = new URLSearchParams(window.location.search);
        return urlParams.get(name);
      }

      const urlParam = getParam("url");
      const decodedURL = decodeURIComponent(urlParam);
      const output = document.getElementById("output");
      output.textContent = decodeVMess(decodedURL);

      const button = document.getElementById("openBtn");
      if (urlParam && urlParam.startsWith("vmess://")) {
        const fullLink = `streisand://import/${urlParam}`;
        button.style.display = "inline-block";
        button.onclick = () => {
          window.location.href = fullLink;
        };
      }
    </script>
  </body>
</html>

