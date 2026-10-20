# Contribuir com encontros

Proponha mudanças por pull request. O repositório `meetings` é a fonte de verdade;
não edite o checkout `.content/meetings` nem copie a definição para o website.

1. Copie `templates/meeting.md` para `meetings/NNN-titulo.md` com identificador
   numerado, em minúsculas e sem acentos (por exemplo, `001-investigando-streams`).
2. Substitua título, resumo e todas as datas ilustrativas. Mantenha `draft: true`
   enquanto prepara a pauta. Confirme acesso, horário e referências antes de publicar.
3. Use Markdown; imagens precisam de texto alternativo. Não use HTML embutido.
4. Coloque anexos em `assets/<id>/` e use `../assets/<id>/arquivo.pdf` no Markdown
   ou em `materials`. PNG, JPEG, WebP, GIF, AVIF, PDF, TXT, CSV e JSON são aceitos.
   Não use links simbólicos. Código versionado pode ficar no repositório e ser
   ligado por URL GitHub; gravações e arquivos grandes ficam em serviços externos.
5. Publique com `draft: false`, após revisão. O merge em `main` dispara o website
   quando o segredo de publicação estiver configurado (ver README).
6. Depois do encontro, acrescente registros e materiais ao mesmo arquivo.
   Não crie uma cópia posterior nem renomeie seu identificador.

## Revisões e calendário

`createdAt` é o instante real de criação da primeira versão e permanece imutável.
Em cada revisão publicada, incremente `sequence` e atualize `updatedAt` para o
instante da alteração (ISO 8601 com offset). Isso inclui mudanças em data, título,
local, participação, materiais ou registros.

Para reagendar, preserve o arquivo, atualize `startsAt`/`endsAt`, guarde a data
anterior em `previousStartsAt` e explique em `changeNotice`. Exija nova revisão.
Se a nova data ainda não é conhecida, mantenha as datas originais como referência,
use `cancelled: true` para retirar essa ocorrência do calendário, explique a
indefinição em `changeNotice` e remova `participationUrl`. Quando confirmar a nova
data, atualize os horários, use `previousStartsAt`, remova o cancelamento e
publique outra revisão, preservando o mesmo identificador.
Para cancelar, use `cancelled: true`, explique em `changeNotice`, incremente
`sequence` e atualize `updatedAt`. Não exclua nem transforme em rascunho um evento
já publicado: a entrada cancelada precisa continuar no feed para os assinantes.

Não use `slug`, `upcoming`, `ongoing`, `finished` ou outros estados derivados do
relógio. A data informa quando ocorre; avisos editoriais registram decisões reais.

A prosa e documentação originais seguem CC BY 4.0 (LICENSE); preserve autoria e
atribuições. Indique licenças próprias para código e materiais de terceiros.
