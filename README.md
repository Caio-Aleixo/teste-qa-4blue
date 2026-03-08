# Teste Técnico - QA Tester - 4blue
Relatório de testes realizado no microssistema de avaliação para a vaga de QA Tester.

Bugs Identificados

----------------------------------------------------------------
Bug 01: [Segurança] Acesso direto à tela interna (Bypass de Login)

* Título: Quebra de controle de acesso (Bypass) via URL /sucesso.

* Descrição: O sistema permite que qualquer usuário visualize a tela de "Login realizado com sucesso" sem a necessidade de autenticação prévia, bastando inserir o caminho da rota diretamente no navegador.

* Passos para reproduzir:
  - Abra o navegador (de preferência em uma aba anônima para garantir que não há cookies).
  - Insira a URL: "https://qa-play-sim.lovable.app/sucesso"
  - Pressione Enter.

* Resultado atual: O sistema carrega e exibe a tela de sucesso com a mensagem "Login realizado com sucesso" e o botão "Sair da conta".

* Resultado esperado: O sistema deve verificar se o usuário possui uma sessão ativa. Caso não esteja logado, deve redirecionar obrigatoriamente para a tela de Login (/).

* Severidade: Crítico (Falha de segurança que expõe áreas restritas).

* Prioridade: Alta (Deve ser corrigido imediatamente para proteger a integridade do sistema).
  
----------------------------------------------------------------
Bug 02: [UI/UX] Layout quebrado nos campos do formulário de cadastro

* Título: Desalinhamento e estouro de margem nos campos "Telefone" e "Confirmar Senha".

* Descrição: Na tela de criação de conta, os campos localizados à direita do formulário não respeitam o limite (padding/width) do container central, sobrepondo-se à área externa do card.

* Passos para reproduzir:
  - Acesse a URL: "https://qa-play-sim.lovable.app/criar-conta"
  - Observe a disposição dos campos "Telefone" (ao lado de Nome Completo) e "Confirmar Senha" (ao lado de Senha).

* Resultado atual: Os inputs da coluna direita estão com a largura estendida para fora do design do card.

* Resultado esperado: Todos os campos devem estar contidos dentro do card central, com espaçamentos (respiros) uniformes nas laterais.

* Severidade: Baixo (Não impede o cadastro, mas prejudica a estética e usabilidade).

* Prioridade: Média (Interface visual é a primeira impressão do usuário).

----------------------------------------------------------------
Bug 03: [Funcional/Segurança] Cadastro permitido sem preenchimento de senhas

* Título: Ausência de obrigatoriedade nos campos de credenciais (Senha).

* Descrição: O sistema permite a conclusão do cadastro mesmo quando os campos de "Senha" e "Confirmar Senha" são deixados totalmente em branco.

* Passos para reproduzir:
  - Acesse a tela de "Criação de Conta".
  - Preencha (ou não) os dados de Nome e E-mail.
  - Deixe os campos Senha e Confirmar Senha vazios.
  - Clique em "Criar Conta".

* Resultado Atual: O sistema exibe a mensagem "Conta criada com sucesso", gerando um usuário sem senha no sistema.

* Resultado Esperado: O sistema deve validar que a senha é um campo obrigatório e impedir o cadastro sem uma definição de credenciais.

* Severidade: Crítica (Um usuário sem senha é uma vulnerabilidade de segurança e um erro lógico de autenticação).

* Prioridade: Alta.

----------------------------------------------------------------
Bug 04: [Regra de Negócio] Violação das regras de Senha

* Título: Falha na validação de complexidade e divergência de senhas.

* Descrição: O sistema ignora a regra exibida na tela (mínimo 8 caracteres e 1 caractere especial) e permite o cadastro com senhas diferentes nos campos "Senha" e "Confirmar Senha".

* Passos para reproduzir:
  - Inserir 1 no campo Senha e A no campo Confirmar Senha.
  - Clique em "Criar Conta".

* Resultado Atual: Conta criada com sucesso.

* Resultado Esperado: Bloqueio do cadastro com alertas de "As senhas não coincidem" e "A senha não atende aos requisitos de segurança".

* Severidade: Crítica.

* Prioridade: Alta.

----------------------------------------------------------------
Bug 05: [Integridade de Dados] Falha de máscara e sanitização de campos

* Título: Aceitação de caracteres inválidos nos campos Nome, Telefone e E-mail.

* Descrição: O sistema não higieniza os dados de entrada, permitindo letras no Telefone, caracteres especiais no Nome e formatos de texto aleatórios no E-mail (sem @ ou domínio).

* Passos para reproduzir:
  - Na tela de cadastro, preencha o Nome com símbolos: %$#@!.
  - Preencha o Telefone com letras: abcde.
  - Preencha o E-mail sem o formato padrão: usuario_sem_arroba.
  - Clique em "Criar Conta".

* Resultado Atual: O sistema aceita os dados inválidos e prossegue para a tela de sucesso.

* Resultado Esperado: Implementar máscaras de entrada no telefone e validação de Regex para nome (apenas letras) e e-mail (formato exemplo@dominio.com).

* Severidade: Médio

* Prioridade: Média

----------------------------------------------------------------
