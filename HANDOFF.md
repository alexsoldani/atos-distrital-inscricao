# Handoff — Atos Itatiaia · Culto na Praia

Documento de transferência para quem for dar continuidade ao projeto (dev, designer ou organização do evento).

**Data do handoff:** 13 de junho de 2026  
**Owner:** Alexandre Soldani  
**URL produção:** https://atos-distrital-inscricao.vercel.app  
**Repositório local:** `~/atos-distrital-inscricao`

---

## 1. Resumo executivo

Foi criada uma **landing page estática** para inscrição no evento **Atos Itatiaia — Culto na Praia** (Distrital), dia **20/06/2026 às 16h** na **Urca, RJ**.

A conversão acontece assim:

```
Visitante → preenche formulário → clica CTA
    → abre WhatsApp (wa.me) com mensagem pronta
    → visitante envia mensagem
    → organização recebe no WhatsApp +55 21 96592-5869
```

**Limitação conhecida:** não existe banco de dados nem planilha automática. Se a pessoa fechar o WhatsApp sem enviar, a inscrição se perde.

---

## 2. Decisões de produto (por que está assim)

### Tom e público
- Culto **jovem**, **aberto a todos** — evitar visual e copy “igrejeiros”.
- Português **pt-BR** com tratamento **você** (nunca *tu/tua*).
- Copy direta: “Garantir minha vaga”, “finaliza pelo WhatsApp”.

### Conversão > estética pesada
- Testamos design **Google Stitch** (Urban Tropic Kinetic): aprovado visualmente, mas **rejeitado em produção** por peso (Tailwind CDN, fontes, animações).
- Versão atual prioriza: **carregamento rápido no celular**, **poucos campos obrigatórios**, **CTA visível**.

### WhatsApp via `wa.me` (grátis)
- Alternativa paga seria WhatsApp Business API.
- Fluxo semi-automático: usuário precisa confirmar envio no app.

### Campos do formulário
| Campo | Obrigatório | Motivo |
|-------|-------------|--------|
| Nome | Sim | Identificação |
| WhatsApp | Sim | Canal principal BR + confirmação |
| E-mail | Não | Reduz fricção |
| Bairro | Não | Opcional, logística |
| Acompanhantes | Não | Opcional |
| Observações | Não | Opcional |
| Consentimento LGPD-lite | Sim | Uso dos dados só para o evento |

---

## 3. Arquitetura técnica

```
┌─────────────────────────────────────┐
│  Vercel (static hosting)            │
│  └── index.html                     │
│  └── assets/*.jpg|png               │
└─────────────────────────────────────┘
           │
           │ (submit)
           ▼
┌─────────────────────────────────────┐
│  JavaScript client-side             │
│  • validação                        │
│  • monta texto da inscrição         │
│  • window.open(wa.me/...)           │
└─────────────────────────────────────┘
           │
           ▼
┌─────────────────────────────────────┐
│  WhatsApp do organizador            │
│  5521965925869                      │
└─────────────────────────────────────┘
```

- **Sem** Node backend, serverless functions, banco ou auth.
- **Sem** variáveis de ambiente na Vercel (número WA está hardcoded no HTML).

---

## 4. Arquivos-chave

| Arquivo | Função |
|---------|--------|
| `index.html` | Toda a aplicação (markup, CSS, JS) |
| `assets/logo-atos-hero.png` | Logo header (recorte sem fundo, 200px) |
| `assets/logo-atos.jpg` | Favicon |
| `assets/logo-culto-praia.jpg` | Logo completa praia (não usada na v3) |
| `.vercel/project.json` | Link projeto ↔ Vercel |
| `outras versões em analise/stitch_*` | Referência design Stitch |

### Constantes para editar

```javascript
// index.html — linha ~script
const WA = "5521965925869";

const EVENT = {
  data: "20/06/2026",
  hora: "16h",
  local: "Urca, Rio de Janeiro"
};
```

### Mensagem WhatsApp (template)

```
🏖️ *Inscrição — Atos Itatiaia · Culto na Praia*

*Nome:* ...
*WhatsApp:* ...
(opcionais: e-mail, bairro, acompanhantes, obs)

📅 20/06/2026 · 16h · Urca, Rio de Janeiro
```

---

## 5. Deploy e acesso

### Vercel
- **Team:** `alexandre-soldanis-projects`
- **Project:** `atos-distrital-inscricao`
- **Project ID:** `prj_sZbOQwgtQudtRIYLMF5UbAsU9ZbG`
- **Alias:** https://atos-distrital-inscricao.vercel.app

### Comandos

```bash
# Deploy produção
cd ~/atos-distrital-inscricao && vercel deploy --prod

# Login (se token expirar)
vercel login
```

### Git (local only)
Repositório git existe **apenas localmente** — não há remote GitHub configurado neste handoff. Para CI/CD automático, conectar repo ao GitHub e integrar na Vercel.

**Commits principais:**
1. `166dd4f` — MVP formulário
2. `aa2ce7c` — WhatsApp
3. `9ca5a31` — Branding logos
4. `2d238ab` — Stitch (descartado como produção final)
5. `43bc7a3` — **v3 atual**

---

## 6. Assets e identidade visual

### Paleta v3 (produção)
| Token | Hex | Uso |
|-------|-----|-----|
| Fundo | `#faf8f5` | Background página |
| Card | `#ffffff` | Formulário |
| Texto | `#1c1410` | Títulos |
| Muted | `#6b5c52` | Subtextos |
| Accent | `#e85d00` | CTA, destaques |

### Paleta Stitch (referência, não em produção)
- Background `#1b110d`, primary-container `#ff6b00`, secondary `#74d5e5`, tertiary `#f9bc48`
- Ver `outras versões em analise/stitch_atos_itatiaia_event_landing/DESIGN.md`

### Logo header
- Gerada a partir de JPG com fundo cinza → PNG transparente via script Pillow em `.venv/`
- Se qualidade do recorte não satisfizer: substituir `assets/logo-atos-hero.png` por export manual (Photoshop, Photoroom, etc.)

### Pendente: hero banner
Foi solicitado prompt JSON (inglês) para gerar **imagem de cabeçalho** com a logo como referência — **ainda não integrada** na página.

---

## 7. O que NÃO foi feito (gaps)

| Gap | Impacto | Recomendação |
|-----|---------|--------------|
| Persistência de inscrições | Alto | Google Sheets via Apps Script ou Formspree |
| Endereço exato + mapa | Médio | Link Waze/Maps no rodapé |
| Instagram URL real | Baixo | Um link no footer |
| Analytics | Médio | Vercel Analytics ou GA4 |
| OG image absoluta | Médio | URL completa para preview social |
| Domínio customizado | Baixo | ex: `inscricao.atositatiaia.org` na Vercel |

---

## 8. Próximos passos recomendados (ordem)

1. **Gerar e integrar hero banner** (IA + logo referência) — se quiser mais impacto visual sem pesar a página (1 imagem WebP otimizada).
2. **Google Sheets** — maior ROI imediato para não depender só do WhatsApp.
3. **Endereço + mapa** — reduz dúvida no dia do evento.
4. **Testar em 3 dispositivos** — iPhone Safari, Android Chrome, desktop.
5. **Divulgar link** — stories, status, grupos.

---

## 9. Prompts JSON gerados (referência)

Durante o projeto foram criados dois prompts JSON em inglês:

1. **Google Stitch** — redesign UI completo (usado; output em `outras versões em analise/`)
2. **Geração de imagem de header** — hero banner com logo como referência, 16:9, tom tropical leve

Guardar cópias desses prompts no Notion/Drive da equipe se forem reutilizar após o evento.

---

## 10. Troubleshooting

| Problema | Solução |
|----------|---------|
| `vercel deploy` pede login | `vercel login` (device flow no browser) |
| WhatsApp não abre no iOS | Safari pode bloquear popup — usuário usa botão “Abrir WhatsApp” na tela de sucesso |
| Logo com halo cinza | Trocar PNG por versão recortada profissionalmente |
| Página antiga em cache | Hard refresh ou aguardar propagação CDN Vercel (~segundos) |
| Inscrição não chegou | Usuário provavelmente não enviou mensagem no WA |

---

## 11. Contatos

| Papel | Detalhe |
|-------|---------|
| WhatsApp inscrições | +55 21 96592-5869 |
| Dev / deploy | Alexandre Soldani |
| Hospedagem | Vercel (`alexandre-soldanis-projects`) |

---

## 12. Checklist de entrega

- [x] Landing publicada
- [x] Formulário funcional
- [x] WhatsApp integrado
- [x] Design leve mobile-first
- [x] Logos no repositório
- [x] README + ROADMAP + HANDOFF
- [ ] Google Sheets / backup inscrições
- [ ] Hero image IA integrada
- [ ] Endereço exato + mapa
- [ ] Analytics
- [ ] Repo remoto GitHub (opcional)

---

*Fim do handoff. Para dúvidas sobre evolução do produto, ver [ROADMAP.md](./ROADMAP.md). Para uso rápido, ver [README.md](./README.md).*