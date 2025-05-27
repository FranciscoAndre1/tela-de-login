<<!DOCTYPE html>
    <html lang="pt-BR">

    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>App de Cadastro</title>
        <link rel="stylesheet" href="style.css">
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css"
            integrity="sha512-9usAa10IRO0HhonpyAIVpjrylPvoDwiPUiKdWk5t3PyolY1cOd4DSE0Ga+ri4AuTroPR5aQvXU9xC6qOPnzFeg=="
            crossorigin="anonymous" referrerpolicy="no-referrer" />
    </head>

    <body>


        </header>

        <main>
            <section class="card registration-card">
                <h2>Cadastrar Usuário</h2>
                <form id="registration-form">
                    <div class="form-group">
                        <label for="reg-nome">Nome:</label>
                        <input type="text" id="reg-nome" name="nome" placeholder="Seu nome completo">
                    </div>
                    <div class="form-group">
                        <label for="reg-cpf">CPF:</label>
                        <input type="text" id="reg-cpf" name="cpf" placeholder="Ex: 123.456.789-00">
                    </div>
                    <div class="form-group">
                        <label for="reg-data-nascimento">Data de Nascimento:</label>
                        <input type="text" id="reg-data-nascimento" name="data-nascimento" placeholder="dd/mm/aaaa">
                    </div>
                    <button type="submit" class="btn btn-primary">Cadastrar</button>
                </form>
            </section>

            <section class="card user-display-card">
                <h2>Usuário Cadastrado</h2>
                <div class="user-info-wrapper">
                    <button class="nav-arrow prev-arrow" aria-label="Usuário anterior" id="prev-user-btn">
                        <i class="fas fa-chevron-left"></i> </button>
                    <div class="user-details">
                        <p>Nome: <span id="display-nome"></span></p>
                        <p>CPF: <span id="display-cpf"></span></p>
                        <p>Data de Nascimento: <span id="display-data-nascimento"></span></p>
                    </div>
                    <button class="nav-arrow next-arrow" aria-label="Próximo usuário" id="next-user-btn">
                        <i class="fas fa-chevron-right"></i> </button>
                </div>
                <button type="button" class="btn btn-danger" id="remove-user-btn">Excluir Cadastro</button>
            </section>
        </main>

        </div>

        <script src="script.js"></script>
    </body>

    </html>
_____________________________________________________________________________________________________________________________


// Acessando os elementos do formulário de cadastro
const registrationForm = document.getElementById('registration-form');
const regNomeInput = document.getElementById('reg-nome');
const regCpfInput = document.getElementById('reg-cpf');
const regDataNascimentoInput = document.getElementById('reg-data-nascimento');
const registerButton = document.querySelector('.btn-primary');

// Acessando os elementos da seção de exibição de usuário
const displayNomeSpan = document.getElementById('display-nome');
const displayCpfSpan = document.getElementById('display-cpf');
const displayDataNascimentoSpan = document.getElementById('display-data-nascimento');

const prevUserButton = document.getElementById('prev-user-btn');
const nextUserButton = document.getElementById('next-user-btn');
const removeUserButton = document.getElementById('remove-user-btn');

// Lista para guardar todos os usuários cadastrados
let users = [];
// Índice do usuário que está sendo exibido no momento
let currentUserIndex = -1; // Começa em -1 porque não há nenhum usuário selecionado inicialmente

// Função para exibir os detalhes de um usuário específico
function displayUser(index) {
    // Se não houver usuários na lista, limpa a exibição e desabilita botões
    if (users.length === 0) {
        displayNomeSpan.textContent = '---';
        displayCpfSpan.textContent = '---';
        displayDataNascimentoSpan.textContent = '---';
        prevUserButton.disabled = true;
        nextUserButton.disabled = true;
        removeUserButton.disabled = true;
        return; // Sai da função, não há usuário para exibir
    }

    // Garante que o índice esteja dentro dos limites válidos da lista
    // Se for menor que 0, volta para o último usuário (circular)
    if (index < 0) {
        index = users.length - 1;
    }
    // Se for maior ou igual ao número de usuários, vai para o primeiro usuário (circular)
    else if (index >= users.length) {
        index = 0;
    }

    currentUserIndex = index; // Atualiza o índice do usuário atual
    const user = users[currentUserIndex]; // Pega o objeto do usuário na lista

    // Atualiza o texto dos spans com os dados do usuário
    displayNomeSpan.textContent = user.nome;
    displayCpfSpan.textContent = user.cpf;
    displayDataNascimentoSpan.textContent = user.dataNascimento;

    // Habilita/desabilita os botões de navegação
    // Se houver apenas 1 ou 0 usuários, os botões de navegação não são necessários
    prevUserButton.disabled = users.length <= 1;
    nextUserButton.disabled = users.length <= 1;
    removeUserButton.disabled = false; // O botão de remover estará sempre habilitado se houver usuários
}

// --- Event Listeners (O que acontece quando algo é clicado ou enviado) ---

// 1. Evento para o envio do formulário de cadastro
registrationForm.addEventListener('submit', function (event) {
    event.preventDefault(); // Impede o comportamento padrão de recarregar a página

    // Cria um novo objeto de usuário com os valores dos inputs
    const newUser = {
        nome: regNomeInput.value,
        cpf: regCpfInput.value,
        dataNascimento: regDataNascimentoInput.value
    };

    users.push(newUser); // Adiciona o novo usuário à lista de usuários

    // Limpa os campos do formulário para o próximo cadastro
    regNomeInput.value = '';
    regCpfInput.value = '';
    regDataNascimentoInput.value = '';

    // Exibe o usuário recém-cadastrado (que é o último da lista)
    displayUser(users.length - 1);
});

// 2. Evento para o botão "Anterior"
prevUserButton.addEventListener('click', function () {
    displayUser(currentUserIndex - 1); // Exibe o usuário anterior na lista
});

// 3. Evento para o botão "Próximo"
nextUserButton.addEventListener('click', function () {
    displayUser(currentUserIndex + 1); // Exibe o próximo usuário na lista
});

// 4. Evento para o botão "Remover Cadastro"
removeUserButton.addEventListener('click', function () {
    // Verifica se há usuários na lista e se um usuário está selecionado
    if (users.length > 0 && currentUserIndex !== -1) {
        // Remove o usuário atual da lista
        // splice(índice, quantidade_a_remover)
        users.splice(currentUserIndex, 1);

        // Ajusta o índice do usuário atual após a remoção
        // Se o usuário removido era o último, o novo índice será o novo último
        if (currentUserIndex >= users.length) {
            currentUserIndex = users.length - 1;
        }

        // Exibe o usuário que está agora no lugar do removido ou limpa a tela
        displayUser(currentUserIndex);
    }
});

// --- Inicialização ---
// Chama displayUser uma vez no início para garantir que a tela de exibição esteja limpa
// e os botões desabilitados se não houver usuários.
displayUser(-1);

////////////////////////////////////////////---------------------------------------------/////////////////////////////////

body {
    font-family: Arial, Helvetica, sans-serif;
    margin: 0;
    padding: 20px;
    /* Adiciona um pouco de espaço ao redor da "tela" */
    display: block;
    align-items: flex-start;
    /* Alinha a tela no topo se o conteúdo for menor que a viewport */
    min-height: 100vh;
    color: #f8e9e9;
    /* Cor padrão do texto */
}

main {
    padding: 20px;
    flex-grow: 1;
}

.card {
    background-color: #524f4e;
    /* Cor de fundo dos cartões */
    padding: 20px;
    margin-bottom: 5px;
    box-shadow: 0 8px 6px rgba(233, 228, 228, 0.664);

}

.card:last-child {
    margin-bottom: 0;
}

.card h2 {
    text-align: flex;
    margin-top: 0;
    margin-bottom: 2px;
    font-size: 1.8em;
    font-weight: 700;
    border-radius: 10cm;
}

.form-group {
    margin-bottom: 10px;
    border-radius: 30px;
}

.form-group label {
    display: block;
    margin-bottom: 10px;
    font-size: 0.80em;
    /* Este tamanho está bem pequeno, talvez queira ajustar */
    color: #f3eaea;
}

input[type="text"],
input[type="date"] {
    /* Aplicado a ambos os tipos */
    width: 100%;
    padding: 10px;
    border: 1px solid #f5f0e7;
    /* Borda sutil */
    border-radius: 30px;
    background-color: #e4e1de;
    /* Cor de fundo dos inputs */
    color: #292828;
    /* Cor do texto dentro dos inputs */
    box-sizing: border-box;
    /* Garante que padding não aumente a largura total */
    font-size: 1em;
}

input[type="text"]::placeholder {
    /* Estilo para o placeholder do campo de data */
    color: #312f2f;
}


/* Para input type="date", o placeholder não é padrão.
   A aparência do seletor de data é controlada pelo navegador.
   Para uma estilização mais customizada, seria necessário JS ou bibliotecas. */
input[type="date"]::-webkit-calendar-picker-indicator {
    filter: invert(1);
    /* Inverte as cores do ícone do calendário em navegadores WebKit */
}


.btn {
    display: block;
    width: 100%;
    padding: 10px;
    border: none;
    border-radius: 8px;
    font-size: 1.1em;
    font-weight: bold;
    color: #ece0e0;
    cursor: pointer;
    text-align: center;
    transition: background-color 0.3s ease;
    margin-top: 10px;
    /* Espaçamento acima do botão */
}

.btn-primary {
    background: linear-gradient(to right, #757271, #575654);
    width: 150px;
    display: flex;
    justify-content: center;
    margin-top: 15px;
}

.btn-primary:hover {
    background: linear-gradient(to right, #777571, #968d8a);
}

.btn-danger {
    background-color: #363433;
    margin-right: 5px;
    width: 15em;
    /* Largura ajustada para o botão de remover */
}

.btn-danger:hover {
    background-color: #1f1818;
}

/* Estilos para a seção de Usuário Cadastrado */
.user-info-wrapper {
    display: flex;
    /* margin-right: 20px;  Essa margem direita pode empurrar o conteúdo, melhor tirar ou ajustar se não for necessário */
    align-items: center;
    border: #eedede;
    /* Isso não define uma borda, apenas a cor. Use border: 1px solid #0f0f0f; se quiser uma borda */
    justify-content: space-between;
    margin-bottom: 15px;
    color: #e9dbdb;
    /* Cor mais clara para o texto de info */
    /* Adicione um espaçamento para o texto "Anterior" e "Próximo" dentro dos botões nav-arrow */
    gap: 2px;
    /* Adiciona um pequeno espaço entre os itens filhos, incluindo os botões */
}

.user-details {
    flex-grow: 1;
    text-align: center;
    /* Centraliza o texto se não houver muito */
    padding: 0 10px;
    /* Espaçamento para não colar nas setas */
}

.user-details p {
    margin: 5px 0;
    font-size: 0.95em;
}



.nav-arrow {
    background-color: rgb(175, 172, 169);
    border: none;
    color: #050505;
    font-size: 1em;
    /* Tamanho das setas */
    padding: 0 10px;
    cursor: pointer;
    font-weight: 800;
    border-radius: 10px;

}

.nav-arrow p {
    /* Estilizando o texto dentro das setas */
    margin: 10;
    /* Remove a margem padrão do parágrafo */
    font-size: 0.8em;
    /* Deixa o texto um pouco menor que a seta */
}

.nav-arrow:hover {
    opacity: 0.7;
    /* Um pouco mais visível do que 0.10 */
}

/* NOVO ESTILO: Para botões desabilitados */
.btn:disabled,
.nav-arrow:disabled {
    opacity: 0.5;
    /* Deixa o botão transparente */
    cursor: not-allowed;
    /* Muda o cursor para "não permitido" */
    background-color: #ccc;
    /* Uma cor de fundo neutra para desabilitado */
    /* Se tiver gradiente, pode ser mais complexo para desabilitar, pode usar um background-image: none; */
}

.btn-danger:disabled {
    background-color: #a0a0a0;
    /* Cor específica para o botão de remover desabilitado */
}

