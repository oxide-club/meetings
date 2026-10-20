# Encontros do Oxide Club

Agenda e arquivo técnico do [Oxide Club](https://oxideclub.dev/encontros/).
Cada encontro tem uma página permanente: a pauta inicial pode receber registros,
slides, experimentos, referências, gravações e transcrições depois da sessão.
Ainda não há encontros publicados; o modelo é somente um rascunho.

```text
meetings/
├── meetings/       # NNN-titulo.md: metadados YAML e conteúdo Markdown
├── assets/         # <id>/anexos pequenos adequados ao Git
├── templates/      # modelo não publicado
└── .github/workflows/deploy-website.yml
```

Leia [CONTRIBUTING.md](CONTRIBUTING.md) para publicar e atualizar encontros.

## Metadados

Obrigatórios: `title`, `summary`, `startsAt`, `endsAt`, `timeZone`, `format` e
`createdAt`. Datas devem ser strings ISO 8601 com offset explícito; `endsAt` deve
ser posterior a `startsAt`. Use um fuso IANA, por exemplo `America/Fortaleza`.
`format` aceita `online`, `presencial` ou `hibrido`. Encontros presenciais ou
híbridos precisam de `location`. `platform` e `participationUrl` são opcionais.
`draft` e `cancelled` têm padrão false; `sequence` começa em 0. Revisões usam
`updatedAt` e `sequence`; reagendamentos usam `previousStartsAt` e `changeNotice`.

`materials` é uma lista opcional de `{title, type, url}`. Tipos: `slides`,
`document`, `code`, `recording`, `transcript` e `reference`. Use URLs HTTPS ou
anexos do próprio encontro. Também é possível apresentar links comentados no
Markdown; evite repetir o mesmo material nos dois lugares. Se não houver
materiais, omita a lista. O identificador vem do nome do arquivo, sem `slug`.

## Prévia e publicação

No checkout do website:

```sh
MEETINGS_SOURCE=/caminho/absoluto/para/meetings npm run dev
```

Esse modo lê alterações locais sem copiar conteúdo; é proibido em CI/produção.
Rascunhos são validados e não geram páginas nem anexos públicos. Para inspecionar
um artigo, use temporariamente `draft: false` somente no checkout local.

O website busca `main` durante a build e valida os metadados por Astro/Zod.
Os arquivos `calendario.ics` individuais e o feed `/encontros/calendario.ics`
são gerados desses mesmos metadados, com UID estável por identificador. Importar
um arquivo individual não garante atualizações; para acompanhá-las, assine o feed
HTTPS no aplicativo de calendário. Frequência de atualização depende do aplicativo.

## Publicação automática

O workflow `Publish website content` reaproveita o mecanismo de `notes` e
`challenges`: pushes em `main` que alteram `meetings/*.md` ou `assets/**` disparam
`oxide-club/oxideclub.dev/.github/workflows/deploy.yml`. Inclui remoções e renomes;
documentação e templates não disparam produção. O primeiro push de inicialização
do repositório também não dispara o website. Não armazene credenciais Cloudflare aqui.

Um mantenedor precisa configurar `WEBSITE_DEPLOY_TOKEN` como Actions secret
neste repositório, usando o mesmo procedimento dos outros repositórios de conteúdo:
token restrito a `oxide-club/oxideclub.dev`, com Actions read/write. O token não
é fornecido por este setup. Sem ele, a publicação automática falha explicitamente.
O workflow do website deve conter a integração de meetings em `main` antes da
primeira publicação de conteúdo. O dispatch confirma o início; acompanhe o
resultado no workflow `Deploy production` do website.

A prosa e documentação originais usam [CC BY 4.0](LICENSE), salvo indicação em
contrário. Código e materiais de terceiros podem ter licenças próprias.
