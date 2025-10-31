# Bug Reports – Beedoo Challenge 2025

Documento com os defeitos encontrados durante a execução dos casos de teste do **Módulo de Curso**.

> Observação: dos 11 casos executados, apenas CT001 passou. Os demais (CT002–CT011) apresentaram falhas e estão documentados abaixo.

---

## 🧩 Metodologia de Teste

A metodologia utilizada foi **Caixa-Preta com abordagem Exploratório e Baseada em Risco**, conforme as práticas do **ISTQB**.  
Essa abordagem foi escolhida porque permite validar o sistema do ponto de vista do usuário, sem necessidade de conhecer o código fonte, focando na experiência real e nas possíveis falhas que impactam diretamente o negócio e a segurança.  
Foram priorizados cenários críticos como:
- Validação de campos obrigatórios;
- Inserção de dados inválidos e limites;
- Tentativas de SQL Injection;
- Quebra de layout (UI/UX);
- Fluxo de cadastro com sucesso.

  

## BUG-002 — Campos obrigatórios não validados (CT002)
**ID do Caso de Teste:** CT002  
**Severidade:** Alta  
**Prioridade:** Alta  
**Ambiente:** Web (Chrome) — 31/10/2025  
**Status:** Aberto

**Passos para reproduzir**
1. Acessar a tela de criação de curso.  
2. Não preencher nenhum campo obrigatório.  
3. Clicar em "Cadastrar Curso".

**Resultado Esperado**  
O sistema deve impedir o cadastro e exibir mensagens de erro específicas em cada campo obrigatório.

**Resultado Obtido**  
O sistema permitiu a criação do curso mesmo com campos obrigatórios vazios e exibiu-o na listagem.

**Recomendação**  
Implementar validação de campos obrigatórios no frontend e no backend; exibir mensagens claras junto aos campos.

---

## BUG-003 — Permite cadastro com nome duplicado (CT003)
**ID do Caso de Teste:** CT003  
**Severidade:** Média/Alta  
**Prioridade:** Média/Alta  
**Ambiente:** Web (Chrome) — 31/10/2025  
**Status:** Aberto

**Passos para reproduzir**
1. Garantir que exista um curso com nome "Curso X".  
2. Acessar a tela de criação de curso.  
3. Preencher todos os campos usando o mesmo nome "Curso X".  
4. Clicar em "Cadastrar Curso".

**Resultado Esperado**  
O sistema deve impedir o cadastro e exibir a mensagem "Já existe um curso com este nome."

**Resultado Obtido**  
O sistema permitiu a criação de outro curso com o mesmo nome e exibiu ambos na listagem.

**Recomendação**  
Adicionar verificação de unicidade no backend e validação no frontend com mensagem de erro adequada.

---

## BUG-004 — URL da imagem não validada (CT004)
**ID do Caso de Teste:** CT004  
**Severidade:** Média  
**Prioridade:** Média  
**Ambiente:** Web (Chrome) — 31/10/2025  
**Status:** Aberto

**Passos para reproduzir**
1. Acessar a tela de criação de curso.  
2. No campo "URL da imagem da capa", inserir `invalid-url` ou uma URL inexistente.  
3. Preencher os demais campos validamente.  
4. Clicar em "Cadastrar Curso".

**Resultado Esperado**  
O sistema deve exibir "URL da imagem inválida" e impedir o cadastro.

**Resultado Obtido**  
O sistema permitiu o cadastro com URL inválida e exibiu o curso na listagem (imagem não carregou corretamente).

**Recomendação**  
Validar sintaxe de URL no frontend; verificar retorno HTTP (200) no backend ou ao renderizar; exibir erro quando necessário.

---

## BUG-005 — Vulnerabilidade XSS armazenada (CT005)
**ID do Caso de Teste:** CT005  
**Severidade:** Crítica  
**Prioridade:** Alta  
**Ambiente:** Web (Chrome) — 31/10/2025  
**Status:** Aberto

**Passos para reproduzir**
1. Acessar o formulário de criação de curso.  
2. No campo "Descrição", inserir `<script>alert('xss')</script>`.  
3. Preencher os demais campos e clicar em "Cadastrar Curso".  
4. Abrir a listagem ou detalhes do curso.

**Resultado Esperado**  
O sistema deve sanitizar a entrada e não executar o script; exibir o texto como literal ou removê-lo.

**Resultado Obtido**  
O sistema aceitou e armazenou o script na descrição (XSS armazenado), havendo execução do script ao renderizar.

**Recomendação**  
Sanitizar e escapar todas as entradas no backend; aplicar políticas de Content Security Policy (CSP); validar também no frontend.

---

## BUG-006 — Cadastro mesmo em modo offline / falha de rede (CT006)
**ID do Caso de Teste:** CT006  
**Severidade:** Alta  
**Prioridade:** Média/Alta  
**Ambiente:** Web (Chrome) — 31/10/2025  
**Status:** Aberto

**Passos para reproduzir**
1. Abrir DevTools → Network → Simular "Offline".  
2. Preencher o formulário de criação de curso.  
3. Clicar em "Cadastrar Curso".

**Resultado Esperado**  
O sistema deve alertar sobre falha de conexão e impedir o cadastro; exibir mensagem amigável.

**Resultado Obtido**  
Mesmo em modo offline, o sistema cadastrou o curso localmente e exibiu na listagem, sem mensagem de erro.

**Recomendação**  
Detectar estado de rede no cliente; bloquear tentativas de POST quando offline; validar transações no backend; exibir mensagens informativas.

---

## BUG-007 — Exclusão: mensagem de sucesso, mas item permanece (CT007)
**ID do Caso de Teste:** CT007  
**Severidade:** Média  
**Prioridade:** Média  
**Ambiente:** Web (Chrome) — 31/10/2025  
**Status:** Aberto

**Passos para reproduzir**
1. Acessar a listagem de cursos.  
2. Clicar em "Excluir Curso" em um item existente.  
3. Confirmar a exclusão.

**Resultado Esperado**  
O curso deve ser removido da listagem e exibir "Curso excluído com sucesso."

**Resultado Obtido**  
A mensagem de sucesso foi exibida, mas o curso permaneceu na listagem (não houve remoção visual/funcional).

**Recomendação**  
Verificar resposta da API de delete; apenas exibir mensagem de sucesso após confirmação do backend; atualizar o estado/refresh da listagem ao excluir.

---

## BUG-008 — Datas inconsistentes aceitas (CT008)
**ID do Caso de Teste:** CT008  
**Severidade:** Média  
**Prioridade:** Média  
**Ambiente:** Web (Chrome) — 31/10/2025  
**Status:** Aberto

**Passos para reproduzir**
1. Acessar formulário de criação.  
2. Inserir Data de Início: 30/12/2025 e Data de Fim: 25/12/2025.  
3. Clicar em "Cadastrar Curso".

**Resultado Esperado**  
O sistema deve impedir o cadastro e exibir "A data de fim deve ser posterior à data de início."

**Resultado Obtido**  
O curso foi cadastrado normalmente, sem validação das datas.

**Recomendação**  
Implementar validação de consistência de datas no frontend e backend.

---

## BUG-009 — Nome aceita caracteres especiais (CT009)
**ID do Caso de Teste:** CT009  
**Severidade:** Baixa/Média  
**Prioridade:** Baixa/Média  
**Ambiente:** Web (Chrome) — 31/10/2025  
**Status:** Aberto

**Passos para reproduzir**
1. Acessar o formulário de criação de curso.  
2. Inserir no campo "Nome do Curso" uma string com caracteres especiais (ex: `Curso!@#$$%`).  
3. Clicar em "Cadastrar Curso".

**Resultado Esperado**  
O sistema deve impedir o cadastro e exibir mensagem solicitando um nome válido (sem caracteres especiais).

**Resultado Obtido**  
O sistema permitiu o cadastro normalmente sem validação.

**Recomendação**  
Definir regex de validação para o campo nome; aplicar validação no backend e frontend.

---

## BUG-010 — Falha em tratar tentativa de SQL Injection (CT010)
**ID do Caso de Teste:** CT010  
**Severidade:** Crítica  
**Prioridade:** Alta  
**Ambiente:** Web (Chrome) — 31/10/2025  
**Status:** Aberto

**Passos para reproduzir**
1. Acessar o formulário de criação de curso.  
2. Inserir `' OR '1'='1` no campo "Nome do Curso".  
3. Clicar em "Cadastrar Curso".

**Resultado Esperado**  
O sistema deve bloquear o cadastro e não interpretar comandos; exibir mensagem de erro.

**Resultado Obtido**  
O sistema permitiu o cadastro com a string maliciosa, o que indica ausência de sanitização/parametrização.

**Recomendação**  
Sanitizar inputs e usar queries parametrizadas/prepared statements no backend; revisar práticas OWASP.

---

## BUG-011 — Layout quebrado com textos muito longos (CT011)
**ID do Caso de Teste:** CT011  
**Severidade:** Média  
**Prioridade:** Média  
**Ambiente:** Web (Chrome) — 31/10/2025  
**Status:** Aberto

**Passos para reproduzir**
1. Inserir 300 caracteres no campo "Nome do Curso".  
2. Inserir 1000 caracteres no campo "Descrição".  
3. Clicar em "Cadastrar Curso".

**Resultado Esperado**  
O sistema deve exibir mensagem "O campo excede o limite máximo de caracteres permitidos." e manter o layout intacto.

**Resultado Obtido**  
O curso foi cadastrado; o texto extravasou a área prevista, quebrando o layout da listagem (problema de UI/UX).

**Recomendação**  
Aplicar limites de caracteres, validação e regras CSS (overflow-wrap, text-overflow: ellipsis) para garantir integridade da UI.

---

## Observações finais
- **Prioridade inicial recomendada:** resolver primeiro as vulnerabilidades de segurança (BUG-005 XSS e BUG-010 SQL Injection) e o problema de validação de campos obrigatórios (BUG-002).  
- **Evidências:** coloquei todos os prints e vídeos no drive com link disponibilizado no README.md

---

