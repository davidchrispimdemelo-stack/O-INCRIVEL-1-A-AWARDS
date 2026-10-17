# Atualização das categorias — 1ºA Awards

A lista foi reduzida de 28 para 21 categorias. A página pública da votação (`docs/index.html`) e a Edge Function (`supabase/functions/awards-api/index.ts`) foram atualizadas para usar os mesmos IDs.

## Sistema de pontos por preferência

Em cada categoria, cada participante pode indicar até duas pessoas diferentes: a primeira opção vale **1 ponto** e a segunda vale **0,5 ponto**. É permitido votar apenas na primeira opção ou pular a categoria; não é permitido preencher apenas a segunda opção nem escolher a mesma pessoa nas duas posições. A classificação e os quatro finalistas são definidos pela soma dos pontos. Cédulas antigas, que só têm uma pessoa por categoria, continuam sendo lidas como primeira opção (1 ponto).

## O que mudou

- As duas categorias centradas em beleza/feiúra foram substituídas por **Mais Icônico(a)** e **Mais Gente Boa**, para manter o tom de brincadeira sem classificar a aparência dos colegas.
- “Mais Mão de Vaca” agora tem descrição coerente com a expressão: economizar bastante.
- Os grupos foram reorganizados em “Polêmicas & sem filtro”, “Vida social & comportamento” e “Clássicos & momentos memoráveis”.

- Foi acrescentada a categoria **Mais Entrosa**, com o ID `mais_entrosa`, tanto na página quanto no servidor.

## Para publicar

1. Atualize os arquivos do projeto no seu repositório.
2. Publique novamente a Edge Function `awards-api` no Supabase para que o servidor aceite os novos IDs.
3. Teste login, envio de voto, apuração da ADM e resultados antes de abrir a votação para a sala.

**Importante:** faça a troca antes de começar a votação, se possível. Votos antigos usam os IDs das categorias anteriores e não devem ser interpretados como votos nas novas categorias. Este pacote altera os arquivos locais; ele não altera automaticamente o projeto já hospedado no GitHub/Supabase.
