# 1ºA Awards 2026 — tutorial completo para iniciantes

**Este tutorial foi feito para quem nunca publicou um site.** Leia uma parte por vez e marque cada etapa quando terminar. Você não precisa entender programação para seguir as instruções, mas precisa copiar os nomes e os comandos com cuidado.

> **Antes de começar:** peça autorização à professora, à coordenação ou a um responsável pela turma. O projeto usa nomes e RAs de estudantes. O site do GitHub Pages fica público na internet. O arquivo com os RAs nunca pode ser publicado.

## Sistema de pontos por preferência

Em cada categoria, cada participante pode indicar até duas pessoas diferentes: a primeira opção vale **1 ponto** e a segunda vale **0,5 ponto**. É permitido votar apenas na primeira opção ou pular a categoria; não é permitido preencher apenas a segunda opção nem escolher a mesma pessoa nas duas posições. A classificação e os quatro finalistas são definidos pela soma dos pontos. Cédulas antigas, que só têm uma pessoa por categoria, continuam sendo lidas como primeira opção (1 ponto).

## O que você vai montar

Pense no projeto como quatro peças:

- **O site (`docs/`)** é a página que os alunos vão abrir no celular ou computador.
- **O Supabase** é o lugar online que guarda o cadastro e os votos.
- **A API (`supabase/functions/awards-api/`)** é o porteiro: verifica o nome e o RA e aplica as regras da votação.
- **O GitHub Pages** dá um endereço para as páginas do site.

## Palavras que podem parecer difíceis

- **PowerShell / terminal:** a janela onde você digita comandos. Parece uma caixa preta ou azul.
- **URL:** o endereço de um site, como `https://supabase.com`.
- **Projeto Supabase:** o espaço online que vai guardar os dados do Awards.
- **Secret / segredo:** uma chave privada. Ela não deve aparecer em páginas públicas.
- **API / `awards-api`:** o porteiro que verifica os acessos e registra os votos.
- **Repositório:** uma pasta de arquivos guardada no GitHub.
- **Project reference:** o código que identifica seu projeto Supabase.

Você não precisa decorar essas palavras. Quando o tutorial pedir uma delas, volte a esta lista. Os nomes dos botões podem aparecer em inglês e podem mudar um pouco; procure o nome mais parecido.

A votação terá duas fases:

1. **Dias 1 a 10:** votação geral. Cada categoria aceita votos em qualquer colega cadastrado.
2. **Dias 11 a 20:** final. Em cada categoria aparecem os quatro colegas mais votados na primeira fase.
3. **Depois de completar os 20 dias:** a votação fecha e os resultados da final aparecem para quem entrar no site.

Se houver empate na quarta vaga da primeira fase, o sistema usa a ordem alfabética para escolher quem entra nos quatro finalistas. Avise a turma dessa regra antes de começar.

---

# PARTE 1 — Deixar os arquivos organizados

## Passo 1. Baixar o projeto

1. Baixe o arquivo `primeiro_a_awards_voto_preferencial.zip` que veio nesta conversa.
2. No computador, abra a pasta **Downloads**.
3. Procure `primeiro_a_awards_voto_preferencial.zip`.
4. Clique nele com o botão direito do mouse.
5. Escolha **Extrair tudo…**.
6. Clique em **Extrair**. O Windows vai criar uma pasta com os arquivos.
7. Abra a pasta extraída `primeiro_a_awards_site`.

Dentro dela, você deve ver pastas como `docs`, `supabase` e `tools`, além de arquivos como `.gitignore` e `README.md`.

## Passo 2. Baixar a lista privada

A lista com os RAs é um arquivo separado do ZIP para diminuir o risco de publicar esses dados por acidente.

1. Baixe o arquivo privado `primeiro_a_awards_roster_privado.json` usando o link fornecido nesta conversa.
2. Baixe também `recados_individuais_privado.sql` pelo link fornecido nesta conversa.
3. Dentro de `primeiro_a_awards_site`, procure a pasta `private`.
4. Se ela **não existir**, crie-a: clique com o botão direito num espaço vazio → **Novo** → **Pasta** → escreva `private` → pressione Enter.
5. Abra a pasta `private`.
6. Copie o arquivo `primeiro_a_awards_roster_privado.json` para dentro dela e renomeie-o para `roster.json`.
7. Copie o arquivo `recados_individuais_privado.sql` para a mesma pasta e renomeie-o para `recados_individuais.sql`.

Os caminhos precisam ficar assim:

```text
primeiro_a_awards_site\private\roster.json
primeiro_a_awards_site\private\recados_individuais.sql
```

Confira o nome com cuidado. O arquivo precisa chamar `roster.json`, não `roster.json.json`.

**Muito importante:**

- Nunca coloque `roster.json` dentro de `docs`.
- Nunca envie `roster.json` ou `recados_individuais.sql` para o GitHub. O segundo arquivo contém os recados particulares dos alunos.
- Não abra e salve esse arquivo no Excel. O Excel pode mexer nos zeros do começo dos RAs.
- Não mande a lista em grupos ou para pessoas que não precisam dela.

## Passo 3. Reconhecer as pastas

No fim desta parte, a pasta deve parecer com isto:

```text
primeiro_a_awards_site
├── docs             ← site público
├── private          ← só no seu computador
│   ├── roster.json  ← lista privada dos alunos
│   └── recados_individuais.sql ← recados privados (baixado separadamente)
├── supabase         ← banco e código do servidor
├── tools            ← programa de importação da lista
├── .gitignore       ← ajuda a impedir envio de arquivos privados
└── README.md        ← explicações do projeto
```

O Windows talvez mostre os itens em uma lista, e não em formato de árvore. Tudo bem. O importante é que as pastas estejam no lugar certo.

---

# PARTE 2 — Instalar dois programas no Windows

Você precisa do **Node.js** para instalar a ferramenta que envia o servidor ao Supabase e do **Python** para importar a lista privada. Faça isso uma vez só neste computador.

## Passo 4. Instalar Node.js

1. Abra o navegador e entre em <https://nodejs.org/en/download>.
2. Procure a versão marcada como **LTS**.
3. Baixe a versão para Windows.
4. Abra o arquivo baixado.
5. Clique em **Next / Avançar** nas telas e aceite as opções padrão. Não precisa mudar as configurações.
6. Quando terminar, feche qualquer janela preta ou azul do terminal que já estava aberta.

Agora confira se instalou:

1. Abra a pasta `primeiro_a_awards_site` no Explorador de Arquivos.
2. Clique uma vez na barra de endereço na parte de cima da janela (onde aparece o caminho da pasta).
3. Apague o que estiver escrito, digite `powershell` e pressione Enter. Vai abrir uma janela de terminal. Ela funciona como uma caixa onde você digita comandos.
4. Digite este comando e pressione Enter:

   ```powershell
   node -v
   ```

5. Deve aparecer um número parecido com `v22...` ou outra versão. O número exato pode ser diferente.
6. Digite:

   ```powershell
   npm -v
   ```

7. Deve aparecer outro número.

Se os dois comandos mostrarem números, está tudo certo. Se aparecer “comando não reconhecido”, feche o terminal, abra outro e tente de novo. Se continuar, confira a instalação do Node.js.

## Passo 5. Instalar a Supabase CLI

Continue na mesma janela do PowerShell. Ela precisa estar aberta dentro da pasta `primeiro_a_awards_site`.

1. Copie esta linha inteira:

   ```powershell
   npm install supabase --save-dev
   ```

2. Cole na janela do PowerShell e pressione Enter.
3. Espere terminar. Pode aparecer bastante texto; isso é normal.
4. Quando voltar a aparecer uma linha pronta para receber outro comando, digite:

   ```powershell
   npx supabase --version
   ```

5. Pressione Enter. Se aparecer um número de versão, a ferramenta foi instalada.

**Dica:** para copiar um comando deste guia, selecione apenas o texto dentro da caixa de código. Não copie os três acentos que aparecem em volta.

## Passo 6. Instalar Python

1. Abra <https://www.python.org/downloads/windows/>.
2. Baixe o instalador recomendado para Windows.
3. Abra o arquivo que baixou e siga as instruções.
4. Se aparecer uma opção chamada **Add Python to PATH** ou **Add python.exe to PATH**, marque essa opção.
5. Termine a instalação.
6. Feche o PowerShell e abra outro dentro da pasta `primeiro_a_awards_site` como explicado no Passo 4.
7. Digite:

   ```powershell
   py --version
   ```

8. Pressione Enter. Deve aparecer `Python 3...` seguido de um número.

Se isso não funcionar, tente `python --version`. Se nenhum comando funcionar, peça ajuda para conferir a instalação antes de continuar.

---

# PARTE 3 — Criar o lugar online que vai guardar os votos

## Passo 7. Criar uma conta no Supabase

1. Entre em <https://supabase.com/>.
2. Crie uma conta e confirme o e-mail, se o site pedir.
3. Entre na conta e clique em **New project**.
4. Dê um nome ao projeto, por exemplo `primeiro-a-awards`.
5. Crie uma senha forte para o banco de dados. **Ela não é o código do ADM.** Guarde-a num local privado.
6. Escolha a região mais próxima que estiver disponível, se aparecer essa escolha.
7. Clique no botão para criar o projeto.
8. Espere o Supabase terminar. Pode levar alguns minutos.

Deixe o projeto aberto no navegador. Não crie outro projeto sem necessidade: todo o site precisa apontar para o mesmo.

## Passo 8. Criar as tabelas

As tabelas são como planilhas organizadas dentro do banco. O arquivo `schema.sql` cria as tabelas e as regras necessárias para guardar os votos.

1. Volte à pasta do projeto no Explorador de Arquivos.
2. Abra `supabase`.
3. Clique com o botão direito no arquivo `schema.sql`.
4. Escolha **Abrir com** → **Bloco de Notas**. Se tiver outro editor de texto, pode usar esse também.
5. Dentro do arquivo, pressione `Ctrl + A` para selecionar tudo.
6. Pressione `Ctrl + C` para copiar.
7. Volte ao navegador, ao painel do seu projeto Supabase.
8. Na barra lateral, procure **SQL Editor**.
9. Clique em **New query** (ou no botão para abrir uma consulta nova).
10. Clique na área grande de texto e pressione `Ctrl + V`.
11. Clique em **Run**.
12. Espere a mensagem de sucesso.

Faça isso **uma única vez em um projeto novo**. Se aparecer erro, pare e peça ajuda; não apague tabelas nem repita comandos aleatoriamente.

## Passo 9. Copiar a URL e a chave pública

O site precisa saber para qual projeto enviar as perguntas. Para isso, usará a URL e uma chave pública.

1. No painel Supabase, procure **Project Settings** ou **Settings**.
2. Entre na área **API Keys** ou abra a área **Connect**, se for a que aparece no seu painel.
3. Copie a **Project URL**. Ela é parecida com `https://abc123.supabase.co`.
4. Copie a chave pública. Nos projetos novos, ela pode começar com `sb_publishable_`; nos antigos, pode se chamar `anon`.
5. Guarde a URL e a chave temporariamente em um bloco de notas **fora da pasta do projeto**. Você vai usar isso duas vezes.

⚠️ **Nunca copie uma chave chamada `secret`, `sb_secret` ou `service_role` para o site.** A chave pública pode ficar no navegador; a chave secreta do servidor, não. Veja a explicação oficial: <https://supabase.com/docs/guides/getting-started/api-keys>.

---

# PARTE 4 — Ligar seu computador ao Supabase

## Passo 10. Fazer login na Supabase CLI

1. Volte à janela do PowerShell aberta dentro de `primeiro_a_awards_site`.
2. Digite:

   ```powershell
   npx supabase login
   ```

3. Pressione Enter.
4. Siga as instruções que aparecerem. Se pedir um token, abra <https://supabase.com/dashboard/account/tokens> no navegador, crie um token pessoal e copie-o para o terminal.
5. Esse token é como uma chave da sua conta. Não o mande para ninguém e não o coloque em arquivos do projeto.

## Passo 11. Ligar a pasta ao projeto certo

1. No Supabase, abra **Project Settings** → **General** (o nome pode mudar um pouco).
2. Procure **Project reference** ou **Reference ID**. É um código curto que identifica o seu projeto.
3. Copie esse código.
4. Volte ao PowerShell. Digite o comando abaixo, mas troque `COLE_AQUI_O_PROJECT_REF` pelo código que copiou:

   ```powershell
   npx supabase link --project-ref COLE_AQUI_O_PROJECT_REF
   ```

5. Pressione Enter.
6. Se pedir a senha do banco, digite a senha que criou no Passo 7. É normal não aparecerem letras enquanto você digita uma senha no terminal.
7. Se terminar sem erro, o computador está conectado ao projeto correto.

Não deixe a palavra `COLE_AQUI_O_PROJECT_REF` no comando. Ela é só um exemplo de onde pôr o código verdadeiro.

---

# PARTE 5 — Criar as chaves privadas do servidor

## Passo 12. Preparar três chaves aleatórias

O servidor precisa de três chaves secretas. Elas não são as senhas dos alunos.

1. No PowerShell, digite o comando abaixo e pressione Enter:

   ```powershell
   [guid]::NewGuid().ToString("N")
   ```

2. Vai aparecer uma linha de letras e números. Copie-a para um bloco de notas que fique **fora da pasta do projeto**.
3. Execute o mesmo comando mais duas vezes. Você precisa de **três linhas diferentes**.
4. Marque-as no seu bloco de notas como `RA_HMAC_SECRET`, `SESSION_SECRET` e `ROSTER_SETUP_KEY`, uma linha para cada nome.

Se o comando der erro, pare e peça ajuda. Não use a mesma linha nas três chaves.

## Passo 13. Guardar as chaves no Supabase

1. Volte ao painel do Supabase.
2. Procure **Edge Functions** e depois **Secrets**, ou uma página chamada **Edge Function Secrets**. O lugar exato pode mudar de acordo com a versão do painel.
3. Procure os campos **Name/Key** e **Value**.
4. Crie estes quatro segredos, escrevendo os nomes exatamente como aparecem aqui:

   | Name/Key (nome) | Value (valor) |
   |---|---|
   | `RA_HMAC_SECRET` | A primeira linha aleatória que você criou |
   | `SESSION_SECRET` | A segunda linha aleatória |
   | `ADMIN_ACCESS_CODE` | O código extra que você escolheu para o ADM. Digite-o somente neste painel privado. |
   | `ROSTER_SETUP_KEY` | A terceira linha aleatória |

5. Clique em **Save**. Se o painel tiver um botão separado para guardar cada segredo, salve todos.
6. Confira se os quatro nomes aparecem na lista. Não precisa nem deve copiar seus valores para o site.

O Supabase já fornece algumas configurações ao servidor automaticamente. Não crie um arquivo público com chaves do servidor e não cole a chave `service_role` em `docs/config.js`.

Guia oficial dos segredos: <https://supabase.com/docs/guides/functions/secrets>.

## Passo 14. Publicar o servidor

1. Volte ao PowerShell, dentro da pasta `primeiro_a_awards_site`.
2. Digite:

   ```powershell
   npx supabase functions deploy awards-api
   ```

3. Pressione Enter e espere a mensagem de sucesso.
4. Se aparecer erro dizendo que a CLI não está conectada ao projeto, volte aos Passos 10 e 11.
5. Se o erro mencionar Docker ou empacotamento, tente:

   ```powershell
   npx supabase functions deploy awards-api --use-api
   ```

6. Se continuar com erro, pare e copie a mensagem de erro para pedir ajuda, mas não copie tokens nem senhas.

A função `awards-api` é o porteiro do site. Ela verifica o login e registra os votos.

Guia oficial: <https://supabase.com/docs/guides/functions/deploy>.

---

# PARTE 6 — Enviar a lista privada ao servidor

## Passo 15. Conferir a lista antes de enviar

Antes de continuar, confirme que este arquivo existe:

```text
primeiro_a_awards_site\private\roster.json
```

Se não existir, volte ao Passo 2. Não copie esse arquivo para `docs`.

## Passo 16. Executar o importador

O importador vai mandar a lista para o Supabase uma única vez. Ele não deve imprimir os RAs no terminal.

1. Na janela do PowerShell, confira se você continua dentro da pasta `primeiro_a_awards_site`.
2. Digite:

   ```powershell
   py tools/import_roster.py
   ```

3. Pressione Enter.
4. Quando pedir `URL do projeto Supabase`, cole a URL que guardou no Passo 9. Ela começa com `https://` e termina com `.supabase.co`. Pressione Enter.
5. Quando pedir a chave pública, cole a chave `sb_publishable_...` ou `anon` que copiou no Passo 9. O texto pode ficar escondido enquanto você cola. Isso é normal. Pressione Enter.
6. Quando pedir `ROSTER_SETUP_KEY`, cole a terceira linha aleatória do Passo 12. Pressione Enter.
7. Espere a resposta. Você deve ver uma mensagem de importação concluída e o número **37**.

Se `py` não funcionar, tente:

```powershell
python tools/import_roster.py
```

### Se a importação der certo

1. Volte ao Supabase → Edge Function Secrets.
2. Apague somente o segredo `ROSTER_SETUP_KEY`, porque ele serviu apenas para a importação inicial.
3. **Não apague** `RA_HMAC_SECRET`, `SESSION_SECRET` ou `ADMIN_ACCESS_CODE`.
4. Guarde a lista original somente em lugar privado, caso seja necessário ter uma cópia de segurança autorizada.

### Se disser que a lista já foi importada

Pare. Não tente importar outra vez, não apague a tabela `students` e não rode o SQL de novo. Essa proteção evita duplicar a turma ou perder os votos.

---

Se aparecer uma mensagem de sucesso indicando que a importação foi concluída, a turma foi cadastrada. Não tente fazer a importação de novo.

## Passo adicional — configurar os recados individuais

O site pode mostrar um recado próprio para cada participante após o login. Para ativar isso sem colocar todos os textos no HTML público:

1. Baixe `recados_individuais_privado.sql` pelo link fornecido nesta conversa, salve-o dentro de `private` com o nome `recados_individuais.sql` e abra-o no Bloco de Notas.
2. No Supabase, abra **SQL Editor** e crie uma consulta nova.
3. Copie o conteúdo do arquivo privado, cole na consulta e clique em **Run**. Faça isso somente depois que a lista dos 37 alunos estiver importada.
4. Publique novamente a Edge Function `awards-api` para ativar a leitura dos recados pelo servidor.
5. Mantenha a pasta `private` fora do GitHub; envie apenas o conteúdo destinado a `docs` para a publicação do site.

Se os recados ainda não forem configurados, a votação continua carregando, mas o cartão de mensagem individual não aparece.

# PARTE 7 — Conectar a página ao banco

## Passo 17. Editar `docs/config.js`

1. Abra a pasta `docs`.
2. Clique com o botão direito em `config.js`.
3. Escolha **Abrir com** → **Bloco de Notas**.
4. Você verá algo parecido com isto:

   ```javascript
   window.AWARDS_CONFIG = {
     SUPABASE_URL: "https://SEU-PROJETO.supabase.co",
     SUPABASE_ANON_KEY: "COLE_SUA_CHAVE_ANON_PUBLICA_AQUI"
   };
   ```

5. Substitua somente `https://SEU-PROJETO.supabase.co` pela URL verdadeira do seu projeto.
6. Substitua somente `COLE_SUA_CHAVE_ANON_PUBLICA_AQUI` pela chave pública que copiou no Passo 9.
7. Deixe as aspas e a vírgula nos mesmos lugares. Não troque o nome `SUPABASE_ANON_KEY`.
8. Pressione `Ctrl + S` para salvar.

A chave deste arquivo é pública. Isso é normal. **Não coloque aqui** `ADMIN_ACCESS_CODE`, `RA_HMAC_SECRET`, `SESSION_SECRET`, `ROSTER_SETUP_KEY`, a chave `secret` ou a chave `service_role`.

---

# PARTE 8 — Publicar a página na internet

O GitHub Pages vai colocar a página no ar. Atenção: o endereço do site será público. A lista de RAs não precisa e não deve estar no GitHub.

## Passo 18. Criar uma conta no GitHub

1. Abra <https://github.com/>.
2. Crie uma conta, se ainda não tiver.
3. Confirme o e-mail, se o site pedir.

## Passo 19. Criar um repositório vazio

Um **repositório** é como uma pasta online para guardar os arquivos do site.

1. No GitHub, clique no `+` no alto da página ou em **New repository**.
2. Dê o nome `primeiro-a-awards`.
3. Para seguir o caminho gratuito do GitHub Pages, talvez seja necessário deixar o repositório **Public**. Isso significa que outras pessoas poderão ver os arquivos que você enviar.
4. Se aparecerem opções para adicionar README, `.gitignore` ou licença, deixe-as desmarcadas para criar o repositório vazio.
5. Clique em **Create repository**.

Não envie o arquivo privado para esse site.

## Passo 20. Instalar o GitHub Desktop e baixar esse repositório vazio

1. Abra <https://desktop.github.com/>.
2. Baixe e instale o GitHub Desktop.
3. Abra o GitHub Desktop e entre na sua conta do GitHub.
4. Volte ao navegador e abra o repositório `primeiro-a-awards` que acabou de criar.
5. Procure o botão **Code**.
6. Escolha **Open with GitHub Desktop**. Se essa opção não aparecer, no GitHub Desktop escolha **File → Clone repository**, encontre `primeiro-a-awards` e clique em **Clone**.
7. Escolha uma pasta fácil de encontrar no computador e confirme.

## Passo 21. Copiar os arquivos públicos para o repositório

Agora você vai copiar o site e o servidor, mas não a lista de RAs.

1. Abra, em duas janelas do Explorador de Arquivos, a pasta original que você extraiu e a pasta que o GitHub Desktop acabou de criar.
2. Na pasta original `primeiro_a_awards_site`, selecione e copie as pastas e arquivos do projeto.
3. Cole o conteúdo dentro da pasta clonada `primeiro-a-awards`.
4. **Não copie** a pasta `private`.
5. **Não copie** a pasta `node_modules`, se ela existir.
6. Copie `.gitignore`, `docs`, `supabase`, `tools`, os arquivos README/guia e `package.json`/`package-lock.json` se existirem. Copie o conteúdo das pastas, sem criar outra pasta `primeiro_a_awards_site` dentro do repositório.
7. Abra o GitHub Desktop. Ele deve mostrar uma lista de mudanças.
8. Procure a lista com calma. Se aparecer `private/roster.json`, **não envie nada**. Volte, apague essa cópia de dentro do repositório e confira se `.gitignore` foi copiado.
9. Nunca coloque código de ADM nem chaves privadas no README, no HTML ou em qualquer arquivo desse repositório.

## Passo 22. Enviar os arquivos ao GitHub

1. No GitHub Desktop, olhe novamente a lista **Changes**.
2. Confirme que a lista privada, senhas e chaves secretas não aparecem.
3. No campo de resumo, escreva `Primeira versão do 1ºA Awards`.
4. Clique em **Commit to main**.
5. Depois clique em **Push origin**.
6. Espere terminar.

A partir desse momento, os arquivos públicos ficam no GitHub. Se perceber que publicou algum segredo ou a lista de RAs, não basta só apagar o arquivo: avise um responsável e troque os segredos afetados.

## Passo 23. Ligar o GitHub Pages

1. No navegador, abra o repositório `primeiro-a-awards`.
2. Clique em **Settings**.
3. Na barra lateral, clique em **Pages**.
4. Procure a parte **Build and deployment**.
5. Em **Source**, selecione **Deploy from a branch**.
6. No campo **Branch**, escolha `main`.
7. No campo da pasta, escolha `/docs`.
8. Clique em **Save**.
9. Espere um pouco e volte à página **Settings → Pages**.
10. O GitHub deverá mostrar o endereço do site. Clique nele para abrir a página.

Se a página mostrar que falta configurar o Supabase, volte ao Passo 17, verifique `docs/config.js`, salve e envie a alteração ao GitHub Desktop.

Guia oficial do GitHub Pages: <https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site>.

---

# PARTE 9 — Conferir tudo antes de começar

**Ainda não aperte o botão que inicia os 20 dias.** Primeiro verifique tudo com calma.

## Passo 24. Testar a página sem começar a votação

1. Abra o endereço do site que o GitHub forneceu.
2. Se a página abrir, confira se o visual está correto.
3. Confira se o site não mostra erro de configuração do Supabase.
4. No campo de nome, entre com o nome completo do ADM exatamente como consta na lista.
5. No campo do RA, digite o RA do ADM **sem o final `SP`**. Preserve todos os zeros do começo e qualquer `X` no fim.
6. No campo de código extra do ADM, digite o código definido em `ADMIN_ACCESS_CODE` no Supabase.
7. Clique em **Acessar votação**.
8. O painel de administrador deve aparecer. Ele mostra os totais da votação, mas não liga uma cédula a um aluno.
9. Confira se há **21 categorias** e **37 participantes**.
10. Antes de iniciar, confira de novo se a votação ainda está fechada.

O site ignora diferenças de maiúsculas/minúsculas e acentos no nome, mas precisa ser o nome certo. Para o RA, retire `SP`, mantenha os zeros iniciais e mantenha um `X` final, se existir.

**Não use a votação real para fazer votos de teste.** Depois que uma cédula é enviada, não há botão para apagá-la. Se quiser testar o envio de votos, faça isso num projeto separado com dados fictícios e autorização de um responsável.

---

# PARTE 10 — Abrir a votação oficial

## Passo 25. Escolher o momento certo

O prazo começa no instante em que você aperta o botão. O site não permite reiniciar a contagem.

1. Combine o dia e a hora com a professora ou com a turma.
2. Avise os alunos sobre as regras, o empate por ordem alfabética e o prazo de 20 dias.
3. Só faça o próximo passo quando estiver pronto para iniciar de verdade.

## Passo 26. Iniciar os 20 dias

1. Entre no site com o login de ADM.
2. Confira que a contagem ainda não começou.
3. Clique em **Abrir votação · iniciar prazo**.
4. Espere a página atualizar.
5. Confira se aparece **Fase 1 — votação geral** e o relógio de contagem regressiva.
6. Compartilhe o endereço do site com a turma somente depois de confirmar que tudo está funcionando e que a escola/responsável autorizou.

### O que acontece depois?

- **Dias 1–10:** votação geral.
- **No 11º dia:** o site passa automaticamente para a final e mostra os quatro mais votados por categoria.
- **Dias 11–20:** os alunos enviam uma nova cédula, agora escolhendo entre os quatro finalistas de cada categoria.
- **Fim do 20º dia:** o site fecha os votos e libera os resultados da final para quem entrar com o login.

Cada aluno pode enviar uma cédula na primeira fase e uma cédula na final. A cédula de uma fase não pode ser editada depois de enviada. O aluno pode pular categorias, mas precisa escolher pelo menos uma categoria para enviar a cédula.

O painel de ADM acompanha quantidades de votos agregadas. Ele não mostra qual aluno votou em qual colega.

---

# PARTE 11 — Se algo não funcionar

### A página diz “Falta configurar docs/config.js”

Abra `docs/config.js`. Confira se colocou a URL correta do projeto e a chave pública correta. Salve com `Ctrl + S`, depois envie a atualização pelo GitHub Desktop.

### O PowerShell diz que `node`, `npm`, `py` ou `python` não existe

Feche o PowerShell e abra uma nova janela. Se continuar, reinstale o programa que falta e marque a opção para adicioná-lo ao PATH, se aparecer.

### O comando `npx supabase` não funciona

Confira se você está dentro da pasta `primeiro_a_awards_site`, onde existe `supabase/config.toml`. Rode outra vez `npm install supabase --save-dev` e depois `npx supabase --version`.

### O login da CLI não funciona

Execute `npx supabase login` de novo e siga as instruções. Nunca coloque o token do Supabase em `docs/config.js` ou no GitHub.

### O deploy da função falhou

Confira se fez login, conectou o projeto correto e salvou os quatro segredos. Tente `npx supabase functions deploy awards-api --use-api` se o erro envolver Docker ou empacotamento. Não inicie a votação até resolver.

### A importação falhou

Confira se existe `private/roster.json`, se a URL e a chave pública estão corretas e se o valor de `ROSTER_SETUP_KEY` é igual ao salvo no Supabase. Se a mensagem disser que a lista já foi importada, pare e não tente de novo.

### Diz “Nome ou RA não confere”

Confira o nome completo e o RA. Digite o RA sem `SP`, preserve os zeros do começo e mantenha um `X` final, se houver.

### O ADM não vê o painel

Confira se o nome é o nome de administrador cadastrado, se o RA está correto e se digitou o código extra igual ao valor privado configurado em `ADMIN_ACCESS_CODE` no Supabase.

### O site continua mostrando a versão velha

No navegador, pressione `Ctrl + F5`. Se não resolver, abra o GitHub Desktop, confira se a última mudança foi enviada com **Push origin** e espere o Pages atualizar.

### A lista privada apareceu no GitHub por engano

Pare de publicar. Remover o arquivo da página não apaga necessariamente seu histórico. Avise um responsável pela turma, remova o acesso público e avalie a troca dos segredos. Não tente esconder o incidente.

---

# PARTE 12 — Checklist final

Marque cada item antes de anunciar a votação:

- [ ] Tenho autorização da escola/responsável para usar os dados dos alunos.
- [ ] A pasta local tem `private/roster.json`.
- [ ] `roster.json` **não** está na pasta `docs`.
- [ ] O banco Supabase foi criado e o `schema.sql` atualizado foi executado.
- [ ] Depois da importação, `private/recados_individuais.sql` foi executado no SQL Editor (o arquivo não foi publicado).
- [ ] Os quatro segredos foram configurados no Supabase.
- [ ] A função `awards-api` foi publicada.
- [ ] O importador confirmou **37 participantes**.
- [ ] Apaguei o segredo temporário `ROSTER_SETUP_KEY` depois da importação.
- [ ] `docs/config.js` tem a URL correta e somente a chave pública.
- [ ] A lista privada, chaves secretas e código do ADM não estão no GitHub.
- [ ] O GitHub Pages está publicando a pasta `/docs`.
- [ ] Entrei como ADM e vi o painel.
- [ ] Expliquei as duas fases e a regra de desempate para a turma.
- [ ] Só agora vou apertar o botão para começar os 20 dias.

## Regras para proteger os colegas

O RA é um identificador escolar, **não é uma senha forte**. Alguém que conheça o nome completo e o RA de outra pessoa pode tentar entrar como ela. Por isso, este site só deve ser usado com autorização explícita da escola ou de um responsável pela turma. Não publique a lista de RAs. GitHub Pages é um site público, mesmo que você pense que ninguém vai encontrar o endereço.

O projeto separa as cédulas dos IDs dos alunos e mostra somente totais, mas isso não é uma promessa de anonimato absoluto: o serviço de hospedagem pode guardar informações técnicas de acesso. Não use esse site para expor segredos, relacionamentos, aparência ou situações que possam humilhar alguém.

## Links oficiais úteis

- Supabase — criar e gerenciar projeto: <https://supabase.com/>
- Supabase — chaves de API: <https://supabase.com/docs/guides/getting-started/api-keys>
- Supabase — segredos das Edge Functions: <https://supabase.com/docs/guides/functions/secrets>
- Supabase — publicar uma Edge Function: <https://supabase.com/docs/guides/functions/deploy>
- Node.js: <https://nodejs.org/en/download>
- Python para Windows: <https://www.python.org/downloads/windows/>
- GitHub Desktop: <https://desktop.github.com/>
- GitHub Pages: <https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site>
