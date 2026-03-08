# teste-qa-4blue
Teste técnico para a etapa de QA Tester na 4blue.

  Para cada bug encontrado, informar:
o Título
o Descrição
o Passos para reproduzir (Pode ser em vídeo – nesse caso coloque o link dele)
o Resultado atual
o Resultado esperado
o Severidade (Crítico / Alto / Médio / Baixo)
o Prioridade (Alta / Média / Baixa)

  Ao final, responder:
o Quais 2 bugs você corrigiria primeiro e por quê?
o Caso tenha, coloque suas sugestões de melhorias para essas telas.

----------------------------------------------------------------
Bug 01: [Segurança] Acesso direto à tela interna (Bypass de Login)

* Título: Quebra de controle de acesso (Bypass) via URL /sucesso.

* Descrição: O sistema permite que qualquer usuário visualize a tela de "Login realizado com sucesso" sem a necessidade de autenticação prévia, bastando inserir o caminho da rota diretamente no navegador.

* Passos para reproduzir:
  - Abra o navegador (de preferência em uma aba anônima para garantir que não há cookies).
  - Insira a URL: [https://qa-play-sim.lovable.app/sucesso](https://qa-play-sim.lovable.app/sucesso)
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
  - Acesse a URL: [https://qa-play-sim.lovable.app/criar-conta](https://qa-play-sim.lovable.app/criar-conta)
  - Observe a disposição dos campos "Telefone" (ao lado de Nome Completo) e "Confirmar Senha" (ao lado de Senha).

* Resultado atual: Os inputs da coluna direita estão com a largura estendida para fora do design do card.

* Resultado esperado: Todos os campos devem estar contidos dentro do card central, com espaçamentos (respiros) uniformes nas laterais.

* Severidade: Baixo (Não impede o cadastro, mas prejudica a estética e usabilidade).

* Prioridade: Média (Interface visual é a primeira impressão do usuário).

----------------------------------------------------------------
