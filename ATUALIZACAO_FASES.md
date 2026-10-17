# Atualização: duas fases da votação

O projeto usa uma contagem total de 20 dias, controlada pelo servidor:

- Dias 1–10: votação geral.
- Dias 11–20: final com os quatro mais votados por categoria na votação geral.
- Depois do 20º dia: os votos fecham e os resultados da final ficam disponíveis para os participantes autenticados.

O desempate pela quarta vaga usa ordem alfabética. Avise a turma antes da votação.

## Sistema de pontos por preferência

Em cada categoria, cada participante pode indicar até duas pessoas diferentes: a primeira opção vale **1 ponto** e a segunda vale **0,5 ponto**. É permitido votar apenas na primeira opção ou pular a categoria; não é permitido preencher apenas a segunda opção nem escolher a mesma pessoa nas duas posições. A classificação e os quatro finalistas são definidos pela soma dos pontos. Cédulas antigas, que só têm uma pessoa por categoria, continuam sendo lidas como primeira opção (1 ponto).

## Como publicar mudanças

1. Atualize os arquivos do projeto no seu repositório local.
2. Dentro da pasta raiz do projeto, abra o PowerShell.
3. Se mudou o código da API, execute `npx supabase functions deploy awards-api`.
4. No GitHub Desktop, confira as mudanças e confirme que `private/roster.json` e segredos não aparecem.
5. Faça Commit e Push. O GitHub Pages publica a versão nova da pasta `/docs`.

Não reinicie o banco, não execute novamente a importação e não inicie o prazo para testar. O contador deve ser iniciado somente uma vez, no momento oficial combinado.
