# 1ºA Awards 2026

Site de votação em duas fases para a turma.

**Siga primeiro `GUIA_COMPLETO.md`, do começo ao fim.** O tutorial explica com passos simples como preparar o computador, criar o projeto Supabase, importar a lista privada, publicar a API e colocar o site no ar.

## Regras da votação

- Dias 1–10: votação geral.
- Dias 11–20: final com os quatro mais votados por categoria.
- Ao fim de 20 dias: votação fechada e resultados da final liberados.

## Pastas principais

- `docs/` — páginas públicas do site.
- `supabase/` — banco de dados e código da API.
- `tools/` — importação inicial da lista privada.
- `private/` — se você criar esta pasta localmente, mantenha-a só no seu computador e nunca a publique.

## Antes de publicar

Peça autorização à escola ou a um responsável pela turma: o projeto usa dados escolares de menores. GitHub Pages é público. Nunca publique a lista `private/roster.json`, segredos do Supabase ou código de administrador. A chave pública em `docs/config.js` é a única chave de API que pode ficar no navegador.

O site ainda precisa ser configurado na sua própria conta Supabase e publicado. Baixar os arquivos não os coloca online automaticamente.
