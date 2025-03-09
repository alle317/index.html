<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sucão do Terceirão</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
            background: #000; /* Fundo preto */
            color: #fff; /* Texto branco */
        }
        h1 {
            font-size: 36px;
            color: #ffa500; /* Laranja vibrante */
            text-shadow: 2px 2px 5px #ff8c00;
        }
        h2 {
            color: #ff8c00;
            font-size: 24px;
            margin-bottom: 20px;
        }
        form {
            display: inline-block;
            text-align: left;
            background: #222;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(255, 165, 0, 0.5);
        }
        input, select {
            width: 100%;
            padding: 8px;
            margin: 5px 0;
            border: 1px solid #ffa500;
            border-radius: 5px;
            background: #333;
            color: white;
        }
        input[type="submit"], button {
            background: #ffa500;
            color: white;
            cursor: pointer;
            font-weight: bold;
            padding: 10px;
            border: none;
            border-radius: 5px;
        }
        input[type="submit"]:hover, button:hover {
            background: #ff8c00;
        }
        .contato {
            margin-top: 20px;
            color: #ffa500;
        }
        #admin-container, #painel-admin {
            margin-top: 40px;
            display: none;
        }
        #pedidos {
            text-align: left;
            background: #222;
            padding: 10px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(255, 165, 0, 0.5);
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <h1>Sucão do Terceirão</h1>
    <h2>Faça já sua encomenda!</h2>

    <form id="pedido-form">
        <label for="nome">Nome:</label>
        <input type="text" id="nome" required>

        <label for="sabor">Escolha o sabor:</label>
        <select id="sabor">
            <option value="Maracujá">Maracujá</option>
            <option value="Laranja">Laranja</option>
        </select>

        <label for="quantidade">Quantidade:</label>
        <input type="number" id="quantidade" min="1" required>

        <label for="observacao">Observação (opcional):</label>
        <input type="text" id="observacao">

        <input type="submit" value="Enviar Pedido">
    </form>

    <div class="contato">
        <p>Para suporte ou dúvidas, entre em contato:</p>
        <p><strong>(28) 99993-8405</strong></p>
    </div>

    <!-- Botão para abrir o login do Admin -->
    <button id="admin-btn">Área do Administrador</button>

    <!-- Login do Administrador -->
    <div id="admin-container">
        <h2>Login do Administrador</h2>
        <form id="admin-login-form">
            <label for="admin-user">Usuário:</label>
            <input type="text" id="admin-user" required>

            <label for="admin-pass">Senha:</label>
            <input type="password" id="admin-pass" required>

            <input type="submit" value="Entrar">
        </form>
    </div>

    <!-- Painel do Administrador -->
    <div id="painel-admin">
        <h2>Pedidos Recebidos</h2>
        <div id="pedidos"></div>
        <button onclick="logout()">Sair</button>
    </div>

    <script>
        // Exibir login ao clicar no botão "Área do Administrador"
        document.getElementById("admin-btn").addEventListener("click", function () {
            document.getElementById("admin-container").style.display = "block";
            this.style.display = "none";
        });

        // Login do administrador
        document.getElementById("admin-login-form").addEventListener("submit", function (event) {
            event.preventDefault();
            let user = document.getElementById("admin-user").value;
            let pass = document.getElementById("admin-pass").value;
            if (user === "alle" && pass === "alepk") {
                document.getElementById("admin-container").style.display = "none";
                document.getElementById("painel-admin").style.display = "block";
                carregarPedidos();
            } else {
                alert("Usuário ou senha incorretos!");
            }
        });

        // Logout do admin
        function logout() {
            document.getElementById("painel-admin").style.display = "none";
            document.getElementById("admin-btn").style.display = "block";
        }

        // Função para salvar pedidos no navegador
        document.getElementById("pedido-form").addEventListener("submit", function (event) {
            event.preventDefault();

            let nome = document.getElementById("nome").value;
            let sabor = document.getElementById("sabor").value;
            let quantidade = document.getElementById("quantidade").value;
            let observacao = document.getElementById("observacao").value;

            let pedido = {
                nome: nome,
                sabor: sabor,
                quantidade: quantidade,
                observacao: observacao
            };

            let pedidos = JSON.parse(localStorage.getItem("pedidos")) || [];
            pedidos.push(pedido);
            localStorage.setItem("pedidos", JSON.stringify(pedidos));

            alert("Pedido enviado com sucesso!");
            document.getElementById("pedido-form").reset();
        });

        // Função para carregar pedidos salvos
        function carregarPedidos() {
            let pedidos = JSON.parse(localStorage.getItem("pedidos")) || [];
            let pedidosDiv = document.getElementById("pedidos");
            pedidosDiv.innerHTML = "";

            if (pedidos.length === 0) {
                pedidosDiv.innerHTML = "<p>Nenhum pedido recebido ainda.</p>";
            } else {
                pedidos.forEach((pedido, index) => {
                    pedidosDiv.innerHTML += `
                        <div>
                            <p><strong>Nome:</strong> ${pedido.nome}</p>
                            <p><strong>Sabor:</strong> ${pedido.sabor}</p>
                            <p><strong>Quantidade:</strong> ${pedido.quantidade}</p>
                            <p><strong>Observação:</strong> ${pedido.observacao}</p>
                            <hr>
                        </div>`;
                });
            }
        }
    </script>

</body>
</html>
