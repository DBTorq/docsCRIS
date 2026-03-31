# CRIS & Bitrix24 API — documentação (Mintlify)

Documentação das APIs do **CRIS** e integração com **Bitrix24**, publicada com [Mintlify](https://mintlify.com).

## Estrutura do repositório

| Caminho | Descrição |
|---------|-----------|
| [`docs-mintlify/docs`](docs-mintlify/docs) | **Raiz do site Mintlify** — `docs.json`, páginas MDX, `logo/`, `favicon.svg` |
| [`CRIS e Bitrix24 API _ Documentação.docx.md`](CRIS%20e%20Bitrix24%20API%20_%20Documenta%C3%A7%C3%A3o.docx.md) | Fonte em Markdown (export) para referência |

## Desenvolvimento local

Instale o [Mintlify CLI](https://www.npmjs.com/package/mint) e execute a partir da pasta do projeto:

```bash
npm i -g mint
cd docs-mintlify/docs
mint dev
```

Abra `http://localhost:3000`.

Verificar links internos:

```bash
cd docs-mintlify/docs
mint broken-links
```

## Publicação (Mintlify Cloud)

Conecte o repositório no [dashboard](https://dashboard.mintlify.com) e defina a **subpasta** do projeto como `docs-mintlify/docs` para que o deploy use apenas esta documentação.

## Recursos

- [Documentação Mintlify](https://mintlify.com/docs)
- Skill para assistentes: `npx skills add https://mintlify.com/docs`

Para contribuir, veja [CONTRIBUTING.md](CONTRIBUTING.md).
