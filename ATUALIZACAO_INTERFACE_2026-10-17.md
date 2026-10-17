# Atualização visual — 17/10/2026

- Seletor de candidatos substitui o menu nativo simples por painel pesquisável.
- Cartões mostram as iniciais e nome escolhido, realce visual, troca e limpeza.
- Barra de progresso registra quantas categorias foram preenchidas.
- Animações de entrada, abertura suave do painel, estados de foco e respeito à preferência de movimento reduzido.
- Responsivo para telas de computador, Android e iPhone.
- Categoria `mais_entrosa` validada para manter o mesmo ID no navegador e na Edge Function.
- Chamada à Edge Function usa a chave publicável no header `apikey`; não trata a chave como JWT de usuário.
- Guia de deploy e ferramenta `tools/check_categories.py` adicionados para evitar divergência entre a lista pública e a lista do servidor.

Testes estáticos executados: sintaxe JavaScript do navegador, leitura de HTML e comparação das 21 categorias entre a página e a função. Ainda é necessário publicar os arquivos no projeto do usuário e testar a integração real no Supabase.

## Sistema de pontos por preferência

Em cada categoria, cada participante pode indicar até duas pessoas diferentes: a primeira opção vale **1 ponto** e a segunda vale **0,5 ponto**. É permitido votar apenas na primeira opção ou pular a categoria; não é permitido preencher apenas a segunda opção nem escolher a mesma pessoa nas duas posições. A classificação e os quatro finalistas são definidos pela soma dos pontos. Cédulas antigas, que só têm uma pessoa por categoria, continuam sendo lidas como primeira opção (1 ponto).
