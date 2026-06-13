# Roadmap — Atos Itatiaia Inscrição

Última atualização: 13 de junho de 2026

## Legenda

- ✅ Concluído
- 🔄 Em progresso / parcial
- 📋 Planejado
- 💡 Ideia / backlog

---

## Fase 1 — MVP de inscrição ✅

| Item | Status | Notas |
|------|--------|-------|
| Formulário de inscrição em pt-BR | ✅ | Tom informal com **você** |
| Validação nome + WhatsApp | ✅ | Máscara BR no telefone |
| Deploy Vercel | ✅ | `atos-distrital-inscricao.vercel.app` |
| Integração WhatsApp `wa.me` | ✅ | Número `5521965925869` |
| Mensagem formatada no envio | ✅ | Markdown compatível com WhatsApp |

---

## Fase 2 — Identidade visual ✅

| Item | Status | Notas |
|------|--------|-------|
| Tom menos “igrejeiro”, mais jovem | ✅ | Culto na Praia, todos bem-vindos |
| Logos oficiais no projeto | ✅ | `logo-culto-praia.jpg`, `logo-atos.jpg` |
| Teste Google Stitch (Urban Tropic Kinetic) | ✅ | Salvo em `outras versões em analise/` |
| Logo ATOS recortada sem fundo | ✅ | `logo-atos-hero.png` (script Pillow) |

---

## Fase 3 — Performance e conversão ✅ (atual)

| Item | Status | Notas |
|------|--------|-------|
| Remover Tailwind CDN + fontes pesadas | ✅ | Página ~14 KB HTML |
| Header só com logo flutuante | ✅ | Substituído depois por hero animado |
| Reduzir campos obrigatórios | ✅ | Nome + WhatsApp apenas |
| Campos extras colapsáveis | ✅ | E-mail, bairro, acompanhantes, obs |
| CTA “Garantir minha vaga” | ✅ | + sticky no mobile |
| Fundo claro (padrão formulário) | ✅ | Foco em conversão |

---

## Fase 4 — Conteúdo e assets 🔄

| Item | Status | Prioridade | Notas |
|------|--------|------------|-------|
| Hero claro/escuro com sol animado | ✅ | Alta | `banner-day.jpg`, `banner-night.jpg`, `sun-scroll.png` |
| Cena de praia com formulário flutuante | 🔄 | Alta | Nova direção local, usando `beach-scene-day.webp` + sol/lua em CSS |
| Substituir/refinar PNG do logo | 📋 | Média | Recorte automático pode ter resíduos de fundo |
| Endereço exato na Urca | 📋 | Alta | Link Google Maps no rodapé |
| Link Instagram real | 📋 | Média | Footer ainda sem URL |
| Favicon em PNG/WebP otimizado | 💡 | Baixa | Hoje usa `logo-atos.jpg` |

---

## Fase 5 — Coleta de dados 📋

| Item | Status | Prioridade | Notas |
|------|--------|------------|-------|
| Google Sheets (respostas automáticas) | 📋 | **Alta** | Hoje só chega via WhatsApp |
| Backup e-mail por inscrição (Formspree) | 💡 | Média | Alternativa ao Sheets |
| Painel admin para ver inscrições | 💡 | Baixa | Só necessário com volume alto |
| API WhatsApp Business (envio automático) | 💡 | Baixa | Tem custo; `wa.me` é grátis |

---

## Fase 6 — Crescimento e CRO 📋

| Item | Status | Prioridade | Notas |
|------|--------|------------|-------|
| Meta Pixel / GA4 (analytics) | 📋 | Média | Medir cliques no CTA e envios WA |
| Página de obrigado com UTM | 💡 | Média | Rastrear origem (Instagram, etc.) |
| Contador regressivo para 20/06 | 💡 | Baixa | Urgência leve |
| A/B teste de CTA | 💡 | Baixa | “Garantir vaga” vs “Quero ir” |
| Open Graph image dedicada | 📋 | Média | Preview ao compartilhar link |

---

## Fase 7 — Experiência avançada 💡 (backlog)

Explorado na conversa, **não implementado** por peso/complexidade:

| Item | Status | Motivo do adiamento |
|------|--------|---------------------|
| Scrollytelling / parallax | 💡 | Prioridade era leveza |
| Confetti / animações pesadas | 💡 | Removido na v3 |
| Design Stitch completo em produção | 💡 | Substituído por versão leve |
| Cursor customizado / magnetic buttons | 💡 | Desktop-only, baixo ROI |

---

## Cronograma sugerido (pré-evento)

```
Até 15/06  → Hero image + endereço/mapa + Instagram
Até 17/06  → Google Sheets OU planilha manual organizada
Até 18/06  → Analytics + testar fluxo em 3 celulares diferentes
19/06      → Divulgação final (stories, WhatsApp)
20/06 16h  → Evento
Pós-evento → Arquivar inscrições + retrospectiva de conversão
```

---

## Métricas de sucesso (sugestão)

| Métrica | Como medir |
|---------|------------|
| Visitas à página | Vercel Analytics ou GA4 |
| Cliques em “Garantir minha vaga” | Evento JS / analytics |
| Mensagens recebidas no WhatsApp | Contagem manual ou etiqueta WA Business |
| Taxa de abandono no formulário | Analytics funil (se implementado) |

---

## Histórico de versões

| Versão | Commit / marco | Descrição |
|--------|----------------|-----------|
| v0 | `166dd4f` | Formulário inicial, tom mais institucional |
| v1 | `aa2ce7c` | WhatsApp wa.me |
| v2 | `9ca5a31` | Logos + paleta Culto na Praia |
| v2.5 | `2d238ab` | Design Stitch (Tailwind, pesado) |
| v3 | `43bc7a3` | Leve, conversão |
| v4 | local | Hero com sol no scroll + formulário leve |
| **v5** | local | **Em validação** — cena de praia, sol/lua e formulário flutuante |
