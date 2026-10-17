# Atualização — voto por preferência (1 ponto + 0,5 ponto)

O site permite duas escolhas diferentes por categoria:

- 1ª opção: 1 ponto.
- 2ª opção: 0,5 ponto.
- A segunda opção só pode ser enviada quando há uma primeira opção.
- A mesma pessoa não pode ocupar as duas posições na mesma categoria.
- Categorias não preenchidas podem ser puladas.
- Os quatro finalistas são escolhidos por pontuação na fase geral; a pontuação da fase final define os resultados finais.

## Arquivos alterados

- `docs/index.html`: interface de votação em duas posições, progresso e pontuação visível.
- `supabase/functions/awards-api/index.ts`: validação no servidor e soma ponderada.

A estrutura da tabela `ballots.votes` já aceita JSON, então não é necessária migração de colunas. Cédulas antigas com apenas um ID por categoria continuam contando como uma primeira opção de 1 ponto.

## Publicar

1. Execute `python tools/check_categories.py`.
2. Publique a função: `npx.cmd supabase functions deploy awards-api`.
3. Publique os arquivos de `docs/` pelo seu provedor do site.
4. Teste primeiro com contas de teste, conferindo uma cédula com 1ª opção e 2ª opção e outra com apenas 1ª opção.

Não execute novamente `schema.sql` apenas por causa dessa atualização; o formato JSONB existente já armazena a nova estrutura.
