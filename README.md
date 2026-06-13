# Atos Itatiaia — Culto na Praia

Landing page de inscrição para o evento **Atos Distrital** (culto jovem na Urca).

**Produção:** https://atos-distrital-inscricao.vercel.app

## Evento

| Campo | Valor |
|-------|--------|
| Nome | Atos Itatiaia — Culto na Praia |
| Data | 20 de junho de 2026 |
| Horário | 16h |
| Local | Urca, Rio de Janeiro |
| Público | Culto jovem, aberto a todos |

## O que a página faz

1. Visitante preenche formulário enxuto (nome + WhatsApp obrigatórios).
2. Ao enviar, abre o **WhatsApp** com mensagem pré-formatada.
3. Visitante confirma a inscrição ao apertar **Enviar** no WhatsApp.
4. Organização recebe os dados no número configurado.

**Não há backend** — inscrições não são salvas em banco/planilha automaticamente.

## Stack

- HTML + CSS + JavaScript vanilla (arquivo único)
- Hospedagem estática na **Vercel**
- Confirmação via link `wa.me` (gratuito, sem API)

## Estrutura do projeto

```
atos-distrital-inscricao/
├── index.html              # Landing page (produção)
├── assets/
│   ├── logo-atos-hero.png  # Logo ATOS recortada (header)
│   ├── logo-atos-hero.jpg  # Original com fundo cinza
│   ├── logo-atos.jpg       # Logo graffiti (favicon / sucesso)
│   └── logo-culto-praia.jpg # Logo Culto na Praia + Itatiaia
├── outras versões em analise/
│   └── stitch_atos_itatiaia_event_landing/  # Export Google Stitch
├── README.md
├── ROADMAP.md
└── HANDOFF.md
```

## Rodar localmente

```bash
cd ~/atos-distrital-inscricao
python3 -m http.server 8080
# Abra http://localhost:8080
```

Ou abra `index.html` direto no navegador.

## Deploy (Vercel)

```bash
cd ~/atos-distrital-inscricao
vercel deploy --prod
```

Requisitos: CLI Vercel instalada e autenticada (`vercel login`).

Projeto Vercel: `alexandre-soldanis-projects/atos-distrital-inscricao`

## Configuração importante

No `index.html`, constante do WhatsApp:

```javascript
const WA = "5521965925869";
```

Formato: código do país + DDD + número, sem `+` ou espaços.

## Design atual (v3 — conversão)

- Fundo claro, formulário branco, sem dependências externas
- Header: apenas logo flutuante (`logo-atos-hero.png`)
- Campos obrigatórios: nome, WhatsApp, consentimento
- Campos opcionais em `<details>` colapsável
- CTA fixo no mobile ao rolar
- Paleta: `--accent: #e85d00`, fundo `#faf8f5`

## Documentação complementar

- [ROADMAP.md](./ROADMAP.md) — evolução e próximos passos
- [HANDOFF.md](./HANDOFF.md) — contexto completo para continuidade

## Contato / organização

- WhatsApp inscrições: **+55 21 96592-5869**
- Responsável técnico: Alexandre Soldani