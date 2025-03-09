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
            background: #000;
            color: #fff;
        }
        h1 {
            font-size: 36px;
            color: #ffa500;
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
        input[type="submit"] {
            background: #ffa500;
            color: white;
            cursor: pointer;
            font-weight: bold;
        }
        input[type="submit"]:hover {
            background: #ff8c00;
        }
        .contato {
            margin-top: 20px;
            color: #ffa500;
        }
        #admin-area {
            display: none;
            background-color: #222;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(255, 165, 0, 0.5);
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <h1>Sucão do Terceirão</h1>
    <h2>Faça já sua encomenda!</h2>

    <form id="order-form">
        <label for="nome">Nome:</label>
        <input type="text" id="nome" name="nome" required>

        <label for="sabor">Escolha o sabor:</label>
        <select id="sabor" name="sabor">
            <option value="maracuja">Maracujá</option>
            <option value="laranja">Laranja</option>
        </select>

        <label for="quantidade">Quantidade:</label>
        <input type="number" id="quantidade" name="quantidade" min="1" required>

        <label for="observacao">Observação (opcional):</label>
        <input type="text" id="observacao" name="observacao">

        <input type="submit" value="Enviar Pedido">
    </form>

    <div class="contato">
        <p>Para suporte ou dúvidas, entre em contato:</p>
        <p><strong>(28) 99993-8405</strong></p>
    </div>

    <div id="admin-area">
        <h2>Pedidos Recebidos</h2>
        <ul id="order-list"></ul>
    </div>

    <script>
        document.getElementById("order-form").addEventListener("submit", function(event) {
            event.preventDefault();

            const nome = document.getElementById("nome").value;
            const sabor = document.getElementById("sabor").value;
            const quantidade = document.getElementById("quantidade").value;
            const observacao = document.getElementById("observacao").value;

            const pedido = {
                nome: nome,
                sabor: sabor,
                quantidade: quantidade,
                observacao: observacao
            };

            let pedidos = JSON.parse(localStorage.getItem("pedidos")) || [];

            pedidos.push(pedido);

            localStorage.setItem("pedidos", JSON.stringify(pedidos));

            document.getElementById("order-form").reset();
            alert("Pedido enviado com sucesso!");

            displayOrders();
        });

        function displayOrders() {
            const pedidos = JSON.parse(localStorage.getItem("pedidos")) || [];
            const orderList = document.getElementById("order-list");

            orderList.innerHTML = '';

            pedidos.forEach((pedido, index) => {
                const li = document.createElement("li");
                li.textContent = `Pedido ${index + 1}: ${pedido.nome} - ${pedido.sabor} - ${pedido.quantidade} unidades`;
                orderList.appendChild(li);
            });
        }

        function loginAdmin() {
            const usuario = prompt("Digite seu usuário:");
            const senha = prompt("Digite sua senha:");

            if (usuario === "alle" && senha === "alepk") {
                alert("Login bem-sucedido!");
                document.getElementById("admin-area").style.display = "block";
                displayOrders();
            } else {
                alert("Usuário ou senha incorretos.");
            }
        }

        loginAdmin();
    </script>

</body>
</html>
