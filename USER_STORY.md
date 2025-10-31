User Story – Módulo de Curso (Beedoo Challenge)
História do Usuário

Como instrutor ou administrador da plataforma
Quero criar cursos e visualizar a listagem de cursos criados
Para disponibilizar conteúdos de aprendizagem aos usuários da plataforma de forma organizada e segura.

Critérios de Aceitação

Deve ser possível cadastrar um novo curso preenchendo os campos nome, descrição, instrutor, URL da imagem da capa, data de início, data de fim, número de vagas e tipo de curso.

Todos os campos obrigatórios devem ter validação e mensagens de erro claras quando não forem preenchidos.

O campo de URL da imagem deve validar se o link inserido é uma URL válida e se a imagem é acessível (retorno HTTP 200).

Após salvar, o curso deve aparecer na listagem de cursos com as informações cadastradas.

O sistema deve impedir cadastros duplicados com o mesmo nome de curso.

Ao clicar em “Excluir Curso”, o sistema deve remover o curso da listagem.

O sistema deve validar entradas de texto para evitar execução de scripts maliciosos (XSS).

Em caso de erros de rede ou servidor, o sistema deve exibir uma mensagem amigável ao usuário (sem códigos técnicos visíveis).

Decisões Tomadas

A User Story foi elaborada após análise exploratória do módulo de curso disponível em:
🔗 https://creative-sherbet-a51eac.netlify.app/

As ações observadas (criar e listar cursos) foram usadas como base para definir os critérios de aceitação.

O formato segue o modelo Ágil (Scrum), utilizando o padrão de User Story + Critérios de Aceitação, para facilitar a rastreabilidade entre requisitos, casos de teste e evidências.

Foram considerados tanto cenários de sucesso (happy path) quanto cenários de erro e vulnerabilidade, visando uma cobertura completa dos testes.

Essa abordagem garante clareza na comunicação com o time de desenvolvimento e permite identificar facilmente comportamentos esperados e não esperados.
