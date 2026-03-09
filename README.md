# Teste Técnico - QA Tester - 4blue
Relatório de testes realizado no microssistema de avaliação para a vaga de QA Tester.

Bugs Identificados:

----------------------------------------------------------------
Bug 01: [Segurança] Acesso direto à tela interna (Bypass de Login)

* Título: Quebra de controle de acesso (Bypass) via URL /sucesso.

* Descrição: O sistema permite que qualquer usuário visualize a tela de "Login realizado com sucesso" sem a necessidade de autenticação prévia, bastando inserir o caminho da rota diretamente no navegador.

* Passos para reproduzir:
  - Abra o navegador (de preferência em uma aba anônima para garantir que não há cookies).
  - Insira a URL: "https://qa-play-sim.lovable.app/sucesso".
  - Pressione Enter.

* Resultado atual: O sistema carrega e exibe a tela de sucesso com a mensagem "Login realizado com sucesso" e o botão "Sair da conta".

* Resultado esperado: O sistema deve verificar se o usuário possui uma sessão ativa. Caso não esteja logado, deve redirecionar obrigatoriamente para a tela de Login (/).

* Severidade: Crítico.

* Prioridade: Alta.
  
----------------------------------------------------------------
Bug 02: [UI/UX] Layout quebrado nos campos do formulário de cadastro

* Título: Desalinhamento e estouro de margem nos campos "Telefone" e "Confirmar Senha".

* Descrição: Na tela de criação de conta, os campos localizados à direita do formulário não respeitam o limite (padding/width) do container central, sobrepondo-se à área externa do card.

* Passos para reproduzir:
  - Acesse a tela de "Criação de Conta": "https://qa-play-sim.lovable.app/criar-conta".
  - Observe a disposição dos campos "Telefone" (ao lado de Nome Completo) e "Confirmar Senha" (ao lado de Senha).

* Resultado atual: Os inputs da coluna direita estão com a largura estendida para fora do design do card.

* Resultado esperado: Todos os campos devem estar contidos dentro do card central, com espaçamentos uniformes nas laterais.

* Severidade: Baixo.

* Prioridade: Média.

----------------------------------------------------------------
Bug 03: [Funcional/Segurança] Cadastro permitido sem preenchimento de senhas

* Título: Ausência de obrigatoriedade nos campos de credenciais (Senha).

* Descrição: O sistema permite a conclusão do cadastro mesmo quando os campos de "Senha" e "Confirmar Senha" são deixados totalmente em branco.

* Passos para reproduzir:
  - Acesse a tela de "Criação de Conta": "https://qa-play-sim.lovable.app/criar-conta".
  - Preencha (ou não) os dados de Nome e E-mail.
  - Deixe os campos Senha e Confirmar Senha vazios.
  - Clique em "Criar Conta".

* Resultado Atual: O sistema exibe a mensagem "Conta criada com sucesso", gerando um usuário sem senha no sistema.

* Resultado Esperado: O sistema deve validar que a senha é um campo obrigatório e impedir o cadastro sem uma definição de credenciais.

* Severidade: Crítico.
  
* Prioridade: Alta.

----------------------------------------------------------------
Bug 04: [Regra de Negócio] Violação das regras de Senha

* Título: Falha na validação de complexidade e divergência de senhas.

* Descrição: O sistema ignora a regra exibida na tela (mínimo 8 caracteres e 1 caractere especial) e permite o cadastro com senhas diferentes nos campos "Senha" e "Confirmar Senha".

* Passos para reproduzir:
  - Acesse a tela de "Criação de Conta": "https://qa-play-sim.lovable.app/criar-conta".
  - Preencha os dados de Nome e E-mail.
  - Inserir "12345678$" no campo Senha e "A" no campo Confirmar Senha.
  - Clique em "Criar Conta".

* Resultado Atual: Conta criada com sucesso.

* Resultado Esperado: Bloqueio do cadastro com alertas de "As senhas não coincidem" e "A senha não atende aos requisitos de segurança".

* Severidade: Crítico.

* Prioridade: Alta.

----------------------------------------------------------------
Bug 05: [Integridade de Dados] Falha na validação de campos (Cadastro)

* Título: Aceitação de tipos de dados inválidos nos campos Nome e E-mail.

* Descrição: O sistema não valida o conteúdo inserido, permitindo que o campo "Nome" aceite símbolos e números, e o campo "E-mail" aceite textos sem o formato padrão de correio eletrônico.

* Passos para reproduzir:
  - Acesse a tela de "Criação de Conta": "https://qa-play-sim.lovable.app/criar-conta".
  - No campo Nome, digite: %$#@!123.
  - No campo E-mail, digite apenas: usuario.
  - Preencha os demais campos e clique em "Criar Conta".

* Resultado Atual: O sistema aceita o cadastro com dados corrompidos/inválidos.

* Resultado Esperado: O sistema deve validar os campos via Regex, permitindo apenas letras no nome e exigindo o formato nome@dominio.com no e-mail.

* Severidade: Médio.

* Prioridade: Média.

----------------------------------------------------------------
Bug 06: [UX/Interface] Ausência de máscaras e validação de formato dos campos

* Título: Falha na validação de tipos de dados e ausência de máscara (Telefone e E-mail).

* Descrição: O sistema não aplica as máscaras nos campos de telefone. O campo Telefone permite a inserção de letras e símbolos sem formatação, enquanto o campo E-mail aceita textos que não seguem a estrutura padrão de correio eletrônico.

* Passos para reproduzir:
  - Acesse a tela de "Criação de Conta": "https://qa-play-sim.lovable.app/criar-conta".
  - No campo Telefone, digite letras (ex: contato_teste).
  - No campo E-mail, digite um texto sem o símbolo "@" ou domínio (ex: meuemail).
  - Clique em "Criar Conta".

* Resultado Atual: O sistema aceita os dados em formatos inválidos e prossegue para a tela de sucesso.

* Resultado Esperado:
  - O campo Telefone deve aceitar apenas números e aplicar a máscara (00) 00000-0000.
  - O campo E-mail deve exigir o formato usuario@dominio.com.

* Severidade: Baixo.

* Prioridade: Baixa.

----------------------------------------------------------------
Bug 07: [Integridade de Dados] Ausência de limite de caracteres (Maxlength)

* Título: Falha na restrição de comprimento de entrada nos campos do formulário.

* Descrição: O sistema não impõe um limite máximo de caracteres (maxlength) nos campos de entrada. Foi verificado que todos os campos permitem a inserção de volumes excessivos de dados (mais de 5.000 caracteres), o que pode causar instabilidade no banco de dados.

* Passos para reproduzir:
  - Acesse a tela de "Criação de Conta": "https://qa-play-sim.lovable.app/criar-conta".
  - Copie um bloco de texto extenso (ex: 5.000 caracteres).
  - Cole este texto em qualquer um dos campos de cadastro.
  - Clique no botão "Criar Conta".

* Resultado Atual: O sistema permite o envio do formulário com milhares de caracteres sem qualquer bloqueio ou alerta.

* Resultado Esperado: Os campos devem possuir um limite máximo razoável (ex: Telefone: 15 caracteres; E-mail: 100 caracteres) para garantir a integridade dos dados.

* Severidade: Médio.

* Prioridade: Baixa.

----------------------------------------------------------------
Bug 08: [Inconsistência/UX] Mensagem de erro inesperada ao realizar login

* Título: Exibição de alerta genérico ou pouco informativo no fluxo de autenticação.

* Descrição: Ao falhar em uma tentativa de login (ou ao interagir com o botão), o sistema retorna uma mensagem de erro "inesperada" (ex: um código técnico, erro em inglês ou popup vazio) em vez de uma instrução amigável.

* Passos para reproduzir:
  - Acesse a tela de Login: "https://qa-play-sim.lovable.app".
  - Insira credenciais inválidas.
  - Clique no botão "Entrar".

* Resultado Atual: O sistema apresenta um alerta com mensagem confusa ou tecnicamente inadequada ("Unexpected error" ou similar).

* Resultado Esperado: O sistema deve exibir uma mensagem clara e amigável, como: "E-mail ou senha inválidos. Por favor, tente novamente."

* Severidade: Baixo.

* Prioridade: Baixa.

----------------------------------------------------------------
Bug 09: [Inconsistência/UX] Mensagem de erro genérica e sem contexto no Login

* Título: Exibição de alerta de "Erro Inesperado" ao executar o login.

* Descrição: Ao interagir com o formulário de login, o sistema apresenta um alerta visual(Notificação) no canto inferior direito com a mensagem "Erro Inesperado". A mensagem não fornece orientações ao usuário sobre o que causou o problema (ex: e-mail inválido, senha incorreta ou falha de conexão).

* Passos para reproduzir:
  - Acesse a tela de Login: "https://qa-play-sim.lovable.app".
  - Realize seu login com dados válidos.
  - Observe o erro apresentado no canto inferior direito da tela.

* Resultado Atual: Uma notificação vermelha surge com o texto "Erro inesperado".

* Resultado Esperado: O sistema deve fornecer mensagens claras e amigáveis de acordo com o erro ocorrido, como: "Usuário não encontrado" ou "Por favor, preencha todos os campos".

* Severidade: Baixo.

* Prioridade: Baixa.

----------------------------------------------------------------
Bug 10: [Inconsistência/UX] Feedback impreciso de credenciais no Login

* Título: Mensagem de erro informando conta inexistente ao colocar e-mail válido com uma senha inválida.

* Descrição: O sistema fornece um feedback falso ao usuário durante o fluxo de login. Ao inserir um e-mail que já consta na base de dados, mas utilizando uma senha divergente, o sistema informa que a conta não está cadastrada, em vez de apontar o erro na senha ou usar uma mensagem genérica de erro de autenticação.

* Passos para reproduzir:
  - Acesse a tela de Login: "https://qa-play-sim.lovable.app".
  - Insira um e-mail válido.
  - Insira uma senha incorreta.
  - Clique no botão "Entrar".

* Resultado Atual: O sistema exibe uma mensagem afirmando que a conta não está cadastrada.

* Resultado Esperado: O sistema deve informar "Senha inválida" ou, seguindo boas práticas de segurança, exibir uma mensagem genérica como: "E-mail ou senha incorretos".

* Severidade: Baixo.

* Prioridade: Baixa.

----------------------------------------------------------------


Quais 2 bugs você corrigiria primeiro e por quê?

  - Bug 01 (Bypass de Login): Por ser uma falha de segurança que compromete toda a aplicação. Permitir acesso à área logada via URL torna qualquer outro esforço de segurança inútil.

  - Bug 04 (Validação de Senha): Para garantir que o usuário não crie uma conta com erro de digitação (senhas diferentes) e que a conta possua um nível mínimo de proteção.

Sugestões de melhorias:

  - Ícone de Visibilidade: Incluir um ícone de "olho" nos campos de senha para que o usuário possa conferir o que digitou.

  - Validação em Tempo Real: Exibir ícones de "Check" ou "Erro" enquanto o usuário preenche os campos, antes mesmo de clicar no botão de enviar.

  - Ao passar o mouse em cima do campo de "e-mail" na tela de criar conta, aparece uma mensagem alegando erro ao colocar 2 "@".

  - Página de 404: Personalizar a página de erro 404 para que ela tenha uma identidade visual da marca.
