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
