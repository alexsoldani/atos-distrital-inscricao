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
│   ├── beach-scene-day.webp # Praia gerada/otimizada para fundo da experiência
│   ├── banner-day.jpg      # Banner claro do topo
│   ├── banner-night.jpg    # Banner escuro do topo
│   ├── sun-scroll.png      # Sol recortado para animação no scroll
│   ├── sun-scroll.jpg      # Original do sol
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

## Design atual (v5 — cena praia + formulário flutuante)

- Cena full-screen com praia gerada, transição dia → pôr do sol → noite
- Sol e lua animados por scroll, controlados em CSS/JS
- Formulário compacto flutuando sobre o cenário
- Campos obrigatórios: nome, WhatsApp, consentimento
- Sem campos opcionais na versão compacta
- Paleta: `--accent: #e85d00`, fundo `#faf8f5`

## Documentação complementar

- [ROADMAP.md](./ROADMAP.md) — evolução e próximos passos
- [HANDOFF.md](./HANDOFF.md) — contexto completo para continuidade

## Contato / organização

- WhatsApp inscrições: **+55 21 96592-5869**
- Responsável técnico: Alexandre Soldani
