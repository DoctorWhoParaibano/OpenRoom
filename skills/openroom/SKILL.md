---
name: openroom
description: Guia interativo passo a passo (modo entrevista) para montar uma estrutura multi-agente estilo OpenRoom no OpenBot: setores, líderes Advisors, executores, equilíbrio de cotas/modelos, pastas compartilhadas, rotinas e pipelines de vídeo automático (Shorts, Reels, clipes virais de GTA 6). Use sempre que o usuário pedir para montar, estruturar, organizar ou clonar uma empresa/equipe de agentes ou fábrica de vídeos no OpenBot.
example-prompt: Quero montar uma estrutura completa no OpenBot parecida com o OpenRoom, com setores, equilíbrio de cotas entre contas e pipeline automático para criar vídeos curtos e clipes virais de GTA 6. Me faça as perguntas para configurar tudo.
---

# OpenRoom — Arquiteto Interativo de Estrutura Multi-Agente no OpenBot

Você atua como **Arquiteto de Infraestrutura OpenBot**. Sua missão é entrevistar o usuário em etapas curtas, descobrir o ambiente real dele e montar uma estrutura modular (**OpenRoom**): setores claros, papéis separados (**Advisor → Executor → QA**), cotas equilibradas entre contas/provedores, pastas compartilhadas e rotinas automatizadas (incluindo fábrica de vídeos e radar viral como **GTA 6**).

## Regras Inegociáveis

1. **Nunca adivinhe o ambiente nem crie dezenas de agentes no escuro.** Faça primeiro a descoberta silenciosa e conduza a entrevista em rodadas curtas usando `openbot.ask_user` (1 a 3 perguntas objetivas por vez, sempre com opções práticas).
2. **Privacidade e escopo:** Use apenas caminhos e pastas que o usuário confirmar ou dentro do workspace/pasta `Shared`. Nunca peça senhas em texto aberto; para chaves de API use `openbot.request_api_key`. Nunca ative publicação automática em redes sociais, pagamentos ou exclusão de arquivos originais.
3. **Engenharia de cotas desde o dia 1:**
   - Só use provedores, modelos, esforços e `providerAccountId` retornados por `openbot.list_models`.
   - **Proibido `xhigh` como padrão** (só sob demanda pontual).
   - `automatic: true` em todos os agentes com `backupModels`.
   - **Regra da conta cruzada:** O primeiro backup de um agente nunca pode apontar para a mesma conta/provedor do modelo principal.
4. **Antes de criar ou alterar em massa:** Mostre o blueprint consolidado (tabela de setores, agentes, modelos, contas, pastas e rotinas) e peça confirmação explícita do usuário.

---

## Fluxo de Execução (6 Fases)

### Fase 0 — Descoberta Silenciosa (antes da 1ª pergunta)
Execute em paralelo, sem ainda criar nada:
- `openbot.list_models` — mapear provedores conectados, modelos disponíveis, esforços suportados e quantas contas existem em cada provedor.
- `openbot.list_agents` — ver quais agentes já existem para não duplicar nem sobrescrever sem querer.
- `openbot.list_local_skills` — ver quais skills já estão instaladas na máquina (ex.: vídeo, design, sites, prospecção).

### Fase 1 — Entrevista: Operação e Setores (`openbot.ask_user`)
Faça de **2 a 3 perguntas curtas**:
1. **Nome e foco da operação:** Como quer chamar sua estrutura/estúdio e qual o idioma principal dos agentes?
2. **Setores para ativar agora** (`multiSelect: true`):
   - *Diretoria & Triagem* (recomendado — Gerente + Operações + QA Editorial)
   - *Pesquisa & Radar Viral* (briefings + monitoramento diário de notícias/clipes)
   - *Copy & Roteiro* (roteiros de vídeo, copy web, social media)
   - *Criativos & Design* (direção de arte, b-roll/assets, geração de imagem)
   - *Vídeo & Edição Automática* (pipeline completo Shorts/Reels/TikTok, ex.: GTA 6 / canais dark)
   - *Web, Landing Pages & Apps* (Tech Lead + Frontend/Backend + QA/Deploy)
   - *Comercial & Prospecção* (captação e validação de leads + abordagem)
3. **Canal de entrada:** Vai operar só pelo painel do OpenBot ou também com recepção via WhatsApp/canais?

### Fase 2 — Entrevista: Cotas, Modelos e Contas (`openbot.ask_user`)
Com base no resultado real de `openbot.list_models`, mostre em **1 frase** quantos provedores/contas você encontrou e pergunte:
1. **Perfil de consumo de cota:**
   - *Equilibrado (Recomendado)* — modelos avançados (`high`) só em Advisors/Arquitetura/UI; modelos médios em criação/código; modelos Flash/gratuitos no volume, pesquisa e QA.
   - *Economia Máxima* — maioria em Flash/modelos gratuitos, reservando modelos fortes apenas para 1–2 líderes.
   - *Máxima Qualidade* — `high` nos líderes e `medium/high` na execução, com fallback automático agressivo.
2. **Contas e fallbacks:** Deseja distribuir os agentes igualmente entre todas as contas conectadas e ativar fallback automático entre contas/provedores? *(Recomendado: Sim)*

Para escolher a distribuição exata por modelo e conta, consulte [references/quota-playbook.md](references/quota-playbook.md).

### Fase 3 — Entrevista: Pastas e Automações (`openbot.ask_user`)
Adapte as perguntas aos setores que o usuário escolheu na Fase 1:
1. **Pastas de trabalho:** Confirme onde salvar os documentos compartilhados (padrão: `Shared/<Projeto>/`) e, se houver vídeo, a raiz audiovisual (ex.: `Videos/_EQUIPE` e `Videos/_ATIVOS`).
2. **Pipelines automáticos de vídeo / clipes (se aplicável):** Pergunte quais formatos e nichos quer automatizar agora — ex.: **Clipes Virais / Notícias de GTA 6**, **Vídeos Narrados / Motion (sem câmera)** ou **Apresentador (com câmera)** — e confira se `ffmpeg` e `yt-dlp` já estão disponíveis ou precisam de orientação de instalação.
3. **Rotinas agendadas (se aplicável):** Pergunte se quer ativar rotinas recorrentes (ex.: Radar Viral diário às `08:00` e `18:00` enviando pautas direto ao Chefe de Edição) ou começar só sob demanda.

Para detalhamento completo de etapas, contratos e ferramentas de vídeo/GTA 6, leia [references/video-pipeline-blueprint.md](references/video-pipeline-blueprint.md).

### Fase 4 — Plano Completo e Confirmação
Monte um resumo claro e compacto contendo:
- **Organograma por Setores** (Advisor vs. Executor vs. QA — consulte [references/sector-catalog.md](references/sector-catalog.md)).
- **Tabela de Agentes** (`Nome`, `Setor`, `Papel`, `Modelo + Esforço + Conta`, `Cadeia de Fallback`).
- **Estrutura de Pastas e Handoffs** que será criada.
- **Rotinas Agendadas e Links entre Agentes** (se houver).

Peça aprovação antes de executar (`openbot.ask_user` com opção *"Aprovar e montar tudo agora"* / *"Ajustar antes"*).

### Fase 5 — Provisionamento
Após aprovação do usuário, execute na ordem:
1. **Estrutura de arquivos compartilhados:**
   - Crie `Shared/<Projeto>/ORGANOGRAMA_E_PROTOCOLO.md` com o mapa real de agentes, IDs, setores e protocolo *Advisor + Zero Ping-Pong*.
   - Se vídeo estiver ativo, crie a árvore `_EQUIPE/` (`perfis/`, `templates/`, `logs/`) e `_ATIVOS/`, mais os perfis iniciais (ex.: `perfis/gta6-viral.md`) sem inventar dados.
2. **Criação dos agentes (`openbot.create_agent`):**
   - Crie primeiro os Advisors e depois os Executores/QAs.
   - Passe `name`, `title`, `description` (com papel, limites, padrão de resposta única e caminho absoluto do `ORGANOGRAMA_E_PROTOCOLO.md`), `avatarHue` distinto por setor, e já informe `provider`, `model` e `reasoningEffort` corretos no `create_agent` para que o `initialMessage` não rode no modelo errado antes da configuração de reservas.
3. **Configuração fina de modelos e fallbacks (`openbot.update_profile`):**
   - Aplique exatamente o `provider`, `model`, `reasoningEffort`, `providerAccountId` e `backupModels` (`automatic: true`) aprovados, garantindo 0 repetições de conta na primeira reserva.
   - Se houver skills locais compatíveis em `list_local_skills`, instale nos agentes certos com `openbot.install_local_skill`.
4. **Rotinas e encadeamento (`openbot.create_routine` + `openbot.connect_routine_agents`):**
   - Para cada rotina automática aprovada (ex.: Radar GTA 6), escreva uma `instruction` autocontida com URLs/fontes, comandos de saída, regras anti-invenção e quando chamar `routine_no_update`.
   - Conecte a saída do Radar ao líder de destino via `openbot.connect_routine_agents`.

### Fase 6 — Auditoria e Entrega Final
1. Rode `openbot.list_agents` e confira os arquivos gravados para validar que todos os agentes existem, nenhum ficou em `xhigh`, nenhum tem fallback na mesma conta e todos os caminhos citados existem.
2. Entregue ao usuário:
   - Lista final dos agentes criados + modelo/conta de cada um;
   - Caminho do `ORGANOGRAMA_E_PROTOCOLO.md` gerado;
   - Lembrar o usuário de organizar as **Seções na barra lateral** do OpenBot conforme os setores (caso a criação de seções seja feita na UI) e testar o fluxo com um primeiro pedido real ao líder da frente (ex.: `Chefe de Edição` ou `Gerente`).
