<input type="text" id="campo" placeholder="Nome de usuário">
<button onclick="buscar()">Pesquisar</button>
<div id="lista"></div>

<script>
    async function buscar() {
        const termo = document.getElementById('campo').value;
        const lista = document.getElementById('lista');
        
        const resposta = await fetch(`https://api.github.com/search/users?q=${termo}`);
        const dados = await resposta.json();

        if (dados.items && dados.items.length > 0) {
            lista.innerHTML = dados.items.map(u => 
                `<div><img src="${u.avatar_url}" width="50"> ${u.login}</div>`
            ).join('');
        } else {
            lista.innerHTML = "Não foram encontrados usuários para esta pesquisa";
        }
    }
</script>
