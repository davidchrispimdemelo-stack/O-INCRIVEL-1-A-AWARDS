# Categoria 21 — Mais Entrosa

A votação agora contém 21 categorias. A categoria **Mais Entrosa** foi acrescentada à página pública e à lista validada pelo servidor com o mesmo ID (`mais_entrosa`).

Descrição exibida: “Consegue puxar assunto, se enturmar e participar das conversas da sala.”

Para publicar, atualize a pasta `docs` e implante novamente a Edge Function `awards-api` no Supabase. Depois, teste a votação antes de divulgar o link. O arquivo local não altera automaticamente o site já hospedado.

## Sistema de pontos por preferência

Em cada categoria, cada participante pode indicar até duas pessoas diferentes: a primeira opção vale **1 ponto** e a segunda vale **0,5 ponto**. É permitido votar apenas na primeira opção ou pular a categoria; não é permitido preencher apenas a segunda opção nem escolher a mesma pessoa nas duas posições. A classificação e os quatro finalistas são definidos pela soma dos pontos. Cédulas antigas, que só têm uma pessoa por categoria, continuam sendo lidas como primeira opção (1 ponto).
