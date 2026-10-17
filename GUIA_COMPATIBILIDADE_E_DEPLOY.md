# Atualização visual, compatibilidade e correção do Mais Entrosa

## Sistema de pontos por preferência

Em cada categoria, cada participante pode indicar até duas pessoas diferentes: a primeira opção vale **1 ponto** e a segunda vale **0,5 ponto**. É permitido votar apenas na primeira opção ou pular a categoria; não é permitido preencher apenas a segunda opção nem escolher a mesma pessoa nas duas posições. A classificação e os quatro finalistas são definidos pela soma dos pontos. Cédulas antigas, que só têm uma pessoa por categoria, continuam sendo lidas como primeira opção (1 ponto).

## O que mudou
- O ID `mais_entrosa` está sincronizado entre `docs/index.html` e `supabase/functions/awards-api/index.ts`.
- O seletor de candidato agora é um painel de seleção com busca por nome, iniciais, confirmação visual, opção de limpar/pular categoria, progresso da cédula e animações suaves.
- A página continua em HTML/CSS/JavaScript sem framework e usa controles `button`, `input` e `fetch`, evitando dependências de APIs específicas de um navegador.
- O layout se reorganiza em uma coluna no celular e duas colunas em telas maiores. Animações são desativadas para usuários que preferem movimento reduzido.
- `docs/config.js` contém apenas a URL do projeto e a chave publicável `sb_publishable_`, não uma chave secreta.
- As chamadas à função enviam a chave publicável no header `apikey` e não a tratam como um token JWT de usuário.

## Publicar na pasta correta
O erro "Há uma escolha inválida na cédula" para Mais Entrosa costuma indicar que a página que enviou `mais_entrosa` e a função publicada no Supabase não estavam na mesma versão. A função do pacote reconhece esse ID.

1. Faça backup da sua pasta de trabalho.
2. Copie os arquivos do pacote por cima da pasta que você realmente usa no PowerShell (no relato anterior: `O-INCRIVEL-1-A-AWARDS`). Mantenha os outros arquivos privados que não fazem parte do pacote; não publique lista de RAs nem SQL de recados no GitHub.
3. Confira `docs/config.js` antes de publicar. A chave `sb_publishable_` é pública; não insira uma `sb_secret_` ou `service_role` no navegador.
4. Antes de publicar, confira se as listas ainda estão sincronizadas executando `python tools/check_categories.py`. O resultado esperado é `OK: 21 categorias sincronizadas` e `OK: Mais Entrosa está presente...`.
5. No PowerShell, entre na pasta do projeto correto e execute:

   ```powershell
   npx.cmd supabase functions deploy awards-api
   ```

6. Publique também a pasta `docs` no mecanismo de hospedagem usado pelo projeto (por exemplo, GitHub Pages via commit/push).
7. Abra a página e faça `Ctrl + F5` no PC. No celular, feche a aba e abra o site novamente, ou recarregue a página.
8. Antes de divulgar para a turma, teste com uma conta de teste e confirme que a categoria Mais Entrosa pode ser selecionada e a cédula é registrada. Não envie outra cédula se o site indicar que a anterior já foi aceita.

## Compatibilidade
Feito para versões atuais de Chrome, Edge, Brave, Safari e navegadores móveis baseados em Chromium/WebKit. O layout adapta-se a PC, Android e iPhone. Não é possível garantir todos os navegadores e versões antigas sem testes em aparelhos reais; faça uma verificação rápida em pelo menos um celular e um computador antes de divulgar.

## O que não muda
As validações de servidor continuam necessárias; não tente corrigir o erro apenas escondendo a mensagem visual. Cada categoria precisa ter o mesmo identificador na página e na Edge Function. A publicação da página e a publicação da Edge Function são passos separados.
