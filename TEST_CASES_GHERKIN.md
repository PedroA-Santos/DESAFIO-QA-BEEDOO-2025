Casos de Teste – Módulo de Curso (Beedoo Challenge)*
 
Cenário 1 – Cadastro de curso com dados válidos

Dado que o usuário está na tela de criação de curso
Quando preencher todos os campos obrigatórios com dados válidos e clicar em “Salvar”
Então o sistema deve cadastrar o curso com sucesso e exibi-lo na listagem de cursos

Cenário 2 – Cadastro com campo obrigatório vazio

Dado que o usuário está na tela de criação de curso
Quando tentar salvar o curso sem preencher um ou mais campos obrigatórios
Então o sistema deve impedir o cadastro e exibir mensagens de erro específicas para cada campo não preenchido

Cenário 3 – Cadastro com nome duplicado

Dado que já existe um curso cadastrado com o mesmo nome
Quando o usuário tentar cadastrar um novo curso com esse mesmo nome
Então o sistema deve impedir o cadastro e exibir a mensagem “Já existe um curso com esse nome.”

Cenário 4 – Validação de URL da imagem inválida

Dado que o usuário está na tela de criação de curso
Quando inserir uma URL de imagem inválida ou inexistente
Então o sistema deve exibir a mensagem “URL da imagem inválida” e impedir o cadastro

Cenário 5 – Validação de segurança (XSS)

Dado que o usuário está na tela de criação de curso
Quando inserir código HTML ou JavaScript em algum campo de texto (ex: <script>alert('xss')</script>)
Então o sistema deve sanitizar a entrada e impedir a execução do script

Cenário 6 – Erro de rede ou servidor

Dado que o usuário preencheu todos os campos corretamente
Quando ocorrer um erro de rede (ex: falha de conexão ou erro 500) ao salvar o curso
Então o sistema deve exibir uma mensagem amigável (“Ocorreu um erro. Tente novamente mais tarde.”)

Cenário 7 – Exclusão de curso

Dado que existe um curso cadastrado na listagem
Quando o usuário clicar em “Excluir Curso” e confirmar a exclusão
Então o curso deve ser removido da listagem e não deve aparecer mais na tela

Cenário 8 – Cancelar exclusão de curso

Dado que o usuário clicou em “Excluir Curso”
Quando o sistema solicitar confirmação e o usuário optar por “Cancelar”
Então o curso deve permanecer na listagem sem alterações

Cenário 9 – Campos de data inválidos

Dado que o usuário está na tela de criação de curso
Quando inserir uma data de fim anterior à data de início
Então o sistema deve impedir o cadastro e exibir a mensagem “A data de fim deve ser posterior à data de início.”
