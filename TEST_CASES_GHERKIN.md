Funcionalidade: Módulo de Curso - Beedoo Challenge 2025
  Como usuário da plataforma
  Quero cadastrar, listar e gerenciar cursos
  Para disponibilizar conteúdos de aprendizagem de forma organizada e segura

  Cenário: CT001 - Cadastro de curso com dados válidos
    Dado que o usuário está na tela de criação de curso
    Quando preencher todos os campos obrigatórios com dados válidos
    E clicar em "Salvar"
    Então o sistema deve cadastrar o curso com sucesso
    E exibir o curso na listagem de cursos

  Cenário: CT002 - Cadastro com campos obrigatórios vazios
    Dado que o usuário está na tela de criação de curso
    Quando tentar salvar o curso sem preencher um ou mais campos obrigatórios
    Então o sistema deve impedir o cadastro
    E exibir mensagens de erro específicas para cada campo não preenchido

  Cenário: CT003 - Cadastro com nome duplicado
    Dado que já existe um curso cadastrado com o mesmo nome
    Quando o usuário tentar cadastrar um novo curso com esse mesmo nome
    Então o sistema deve impedir o cadastro
    E exibir a mensagem "Já existe um curso com este nome."

  Cenário: CT004 - Validação de URL da imagem inválida
    Dado que o usuário está na tela de criação de curso
    Quando inserir uma URL de imagem inválida ou inexistente no campo "URL da imagem da capa"
    Então o sistema deve exibir a mensagem "URL da imagem inválida"
    E impedir o cadastro do curso

  Cenário: CT005 - Validação de segurança contra XSS
    Dado que o usuário está na tela de criação de curso
    Quando inserir o código abaixo em qualquer campo de texto:
      """
      <script>alert('xss')</script>
      """
    E clicar em "Cadastrar Curso"
    Então o sistema deve sanitizar a entrada
    E impedir a execução do código JavaScript

  Cenário: CT006 - Erro de rede ou servidor ao salvar
    Dado que o usuário preencheu todos os campos corretamente
    Quando ocorrer uma falha de rede ou erro 500 ao salvar o curso
    Então o sistema deve exibir a mensagem "Ocorreu um erro. Tente novamente mais tarde."
    E não cadastrar o curso

  Cenário: CT007 - Exclusão de curso
    Dado que existe um curso cadastrado na listagem
    Quando o usuário clicar em "Excluir Curso" e confirmar a exclusão
    Então o curso deve ser removido da listagem
    E o sistema deve exibir a mensagem "Curso excluído com sucesso."

  Cenário: CT008 - Campos de data inválidos
    Dado que o usuário está na tela de criação de curso
    Quando inserir uma data de fim anterior à data de início
    E clicar em "Cadastrar Curso"
    Então o sistema deve impedir o cadastro
    E exibir a mensagem "A data de fim deve ser posterior à data de início."

  Cenário: CT009 - Cadastro com caracteres especiais no nome
    Dado que o usuário está na tela de criação de curso
    Quando preencher o campo "Nome do Curso" com caracteres especiais (ex: @ # $ % & * )
    E clicar em "Cadastrar Curso"
    Então o sistema deve impedir o cadastro
    E exibir a mensagem "Insira um nome válido (sem caracteres especiais)."

  Cenário: CT010 - Teste de SQL Injection
    Dado que o usuário está na tela de criação de curso
    Quando inserir o valor "' OR '1'='1" no campo "Nome do Curso"
    E clicar em "Cadastrar Curso"
    Então o sistema deve bloquear o cadastro
    E exibir a mensagem "O nome do curso contém caracteres inválidos."
    E não interpretar nenhum comando SQL

  Cenário: CT011 - Limite de caracteres em campos (nome/descrição)
    Dado que o usuário está na tela de criação de curso
    Quando preencher o campo "Nome do Curso" com mais de 300 caracteres
    E preencher o campo "Descrição" com mais de 1000 caracteres
    E clicar em "Cadastrar Curso"
    Então o sistema deve impedir o cadastro
    E exibir a mensagem "O campo excede o limite máximo de caracteres permitidos."
    E o layout da listagem deve permanecer intacto (sem quebra de UI)
