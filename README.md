
<html lang="pt-br">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lista Responsiva</title>
    <link href="css/bootstrap.min.css" rel="stylesheet">
    <style>
        html, body {
            height: 100%;
            margin: 0;
            width: 100%;
        }

        .parallax {
            background: linear-gradient(135deg, #3498db, #8e44ad);
            position: fixed; /* Usa posição fixa para a imagem de fundo */
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-size: cover; /* Faz com que a imagem cubra todo o elemento */
            background-attachment: fixed; /* Garante que a imagem não se mova ao rolar */
            background-position: center; /* Centraliza a imagem */
            overflow: hidden;
            will-change: transform;
            z-index: -1;
        }

        .content {
            position: relative;
            z-index: 1;
            padding: 20px;
        }

        .shadow-lg {
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        .rounded {
            border-radius: .25rem;
        }

        .lista img {
            max-width: 100%; /* Faz com que a imagem não ultrapasse a largura do contêiner */
            height: auto; /* Mantém a proporção da imagem */
            display: block;
            margin: 0 auto; /* Centraliza a imagem horizontalmente */
        }

        details {
            margin-bottom: 15px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: .25rem;
        }

        button {
            cursor: pointer;
        }
    </style>
</head>

<body>
    <div class="parallax"></div>

    <div class="content">
        <div class="container text-center">
            <div class="row align-items-center">
                <div class="col"></div>
                <div class="col" style="height:297px;"></div>
                <div class="col"></div>
            </div>
        </div>

        <div class="container text-center">
            <div class="row align-items-center d-flex">
                <div class="col"></div>
                <div class="col shadow-lg rounded" style="background-color: #ffff; padding: 10px;">
                    <div class="lista">
                        <h2>Lista</h2>
                        <h5>Título: <input class="shadow rounded" type="text" id="Titulo" placeholder="Digite aqui"></h5><br>
                        <h5>Descrição: <input class="shadow rounded" type="text" id="Descricao" placeholder="Digite aqui"></h5><br>
                        <input class="border rounded shadow" type="file" id="imagem" placeholder="Selecione uma imagem"><br><br>
                        <button class="border rounded shadow btn btn-success" onclick="adicionarItem('compras')">Adicionar</button><br><br>
                        <div class="justify-content-start" id="listaCompras"></div>
                    </div>
                </div>
                <div class="col"></div>
            </div>
        </div>
    </div>

    <script>
        function adicionarItem(tipoLista) {
            let inputTitulo, inputDescricao, listaId, imagemInput;
            switch (tipoLista) {
                case 'compras':
                    inputTitulo = document.getElementById('Titulo').value.trim();
                    inputDescricao = document.getElementById('Descricao').value.trim();
                    listaId = 'listaCompras';
                    imagemInput = document.getElementById('imagem').files[0]; // Captura o arquivo de imagem
                    break;
                default:
                    return;
            }

            if (inputTitulo !== '' && inputDescricao !== '') {
                const lista = document.getElementById(listaId);

                // Criar o elemento details
                const detalhes = document.createElement('details');
                detalhes.className ='shadow';
                const resumo = document.createElement('summary');
                resumo.className = 'grid gap-3';
                resumo.textContent = inputTitulo; // O título vai no summary
                detalhes.appendChild(resumo);

                // Adicionar a descrição como conteúdo do details
                const descricao = document.createElement('p');
                descricao.textContent = inputDescricao;
                detalhes.appendChild(descricao);

                // Adicionar a imagem se estiver presente
                if (imagemInput) {
                    const reader = new FileReader();
                    reader.onload = function (e) {
                        const imagem = document.createElement('img');   
                        imagem.src = e.target.result;
                        detalhes.appendChild(imagem);
                    };
                    reader.readAsDataURL(imagemInput);
                }

                // Adicionar o botão de remoção
                const botaoRemover = document.createElement('button');
                botaoRemover.className = 'rounded border shadow btn btn-outline-danger';
                botaoRemover.textContent = 'Remover';
                botaoRemover.onclick = function () {
                    lista.removeChild(detalhes);
                };
                detalhes.appendChild(botaoRemover);

                // Adicionar os detalhes à lista
                lista.appendChild(detalhes);

                // Limpar os campos de entrada
                document.getElementById('Titulo').value = '';
                document.getElementById('Descricao').value = '';
                document.getElementById('imagem').value = ''; // Limpar o campo de arquivo
            }
        }
    </script>
</body>

</html>