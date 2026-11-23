# Catálogo Modular de Setores e Agentes — OpenRoom

Use este catálogo na Fase 4 da entrevista para montar apenas os setores que o usuário escolheu. Não crie agentes ociosos para setores não selecionados.

---

## Regras de Desenho de Agentes
- **Separação de papéis:**
  - **Advisor (Líder):** Planeja ponta a ponta, define critérios de aceite, envia 1 pedido autocontido ao time (Zero Re-consulta) e revisa a entrega final. Nunca faz trabalho braçal repetitivo.
  - **Executor:** Executa o plano aprovado com precisão (Zero Ping-Pong: só pergunta se faltar dado bloqueante, tudo numa única lista).
  - **QA Independente:** Audita com evidência mensurável (comandos, `ffprobe`, LUFS, Lighthouse, suíte de testes). Nunca corrige no lugar do executor nem aprova sem prova.
- **Cores sugeridas na barra lateral (`avatarHue`):** `0` vermelho (Diretoria/Infra), `215` azul (Pesquisa), `30` laranja (Copy), `280` violeta (Criativos/Direção), `320` magenta (Edição/Motion), `185` ciano (Frontend/Web), `150` verde (Triagem/Backend), `100` lima (QA/Leads).

---

## 1. Diretoria & Operações
- **Supervisor** (`Advisor / Infra`, `avatarHue: 0`)
  - *Papel:* Governança do OpenBot, cotas, modelos reservas, skills e arquitetura entre setores.
  - *Tier:* Médio/Alto (`high`).
- **Gerente** (`Advisor / Orquestrador`, `avatarHue: 0`)
  - *Papel:* Recebe demandas amplas do dono, define prioridades, coordena setores sem misturar marcas e revisa a entrega final.
  - *Tier:* Alto (`high`).
- **Triagem / Recepção WhatsApp** *(opcional)* (`Executor / Roteador`, `avatarHue: 150`)
  - *Papel:* Responde dúvidas simples e encaminha tarefas longas ao líder certo com contexto completo.
  - *Tier:* Econômico (`medium` / Flash).
- **Operações** *(opcional)* (`Executor`, `avatarHue: 215`)
  - *Papel:* Escopo, cronograma, custos e capacidade com base apenas em dados confirmados.
  - *Tier:* Gratuito / Econômico (`low`).
- **QA Editorial & Entregas** *(opcional)* (`QA Independente`, `avatarHue: 100`)
  - *Papel:* Revisa textos, PDFs, carrosséis e propostas antes de entregar ao cliente/usuário.
  - *Tier:* Econômico (`high` em Flash ou gratuito).

---

## 2. Pesquisa & Inteligência
- **Briefing & Pesquisa** (`Executor`, `avatarHue: 215`)
  - *Papel:* Transforma links, pastas ou briefings soltos em `briefing.md` verificável; todo dado sem fonte vai marcado `a confirmar`.
  - *Tier:* Econômico (`high` em Flash).
- **Radar Viral (Clipes & Notícias — ex.: GTA 6)** *(ativar se houver canal/vídeo automático)* (`Executor Agendado`, `avatarHue: 320`)
  - *Papel:* Monitora notícias verificadas e clipes em alta com fonte/URL, baixa e corta em `9:16` (`1080×1920`) na pasta `_RADAR/AAAA-MM-DD/` e classifica gancho (`Clipe + Motion` vs. `Roteiro + Motion`), entregando ao `Chefe de Edição`.
  - *Tier:* Econômico (`high` em Flash).

---

## 3. Copy & Roteiro
- **Roteirista de Vídeo** *(se houver vídeo)* (`Executor`, `avatarHue: 215`)
  - *Papel:* Converte `briefing.md` ou pacote do Radar em `Docs/roteiro.md` (Gancho, Dor/Contexto, Demo/Desenvolvimento, Prova, CTA) + `Docs/narracao_vNN.md` pronto para TTS/gravação.
  - *Tier:* Econômico (`high` em Flash).
- **Copy & Estrutura Web** *(se houver sites)* (`Executor`, `avatarHue: 30`)
  - *Papel:* Cria `copy.md` seção por seção, H1, CTAs, metadados SEO e alt text sem clichês artificiais.
  - *Tier:* Médio (`medium`).
- **Conteúdo Social / Editorial** *(se houver social media)* (`Executor`, `avatarHue: 30`)
  - *Papel:* Calendários editoriais, legendas e roteiros de carrossel com voz humana.
  - *Tier:* Médio/Alto (`medium` ou `high`).

---

## 4. Criativos & Design
- **Direção de Arte & UI** (`Advisor Criativo`, `avatarHue: 280`)
  - *Papel:* Define identidade visual autoral (`design.md`: conceito, paleta hex, tipografia, grid e motion).
  - *Tier:* Avançado/UI (`high`).
- **Cenas e Imagens (B-Roll & Telas Reais)** (`Executor`, `avatarHue: 150`)
  - *Papel:* Coleta telas reais, logos oficiais e B-rolls sem marca d'água, registrando origem, resolução e licença em `_CLAUDE/assets_escolhidos.md`.
  - *Tier:* Econômico (`high` em Flash).
- **Gerador de Imagens** *(opcional)* (`Executor IA`, `avatarHue: 280`)
  - *Papel:* Gera ilustrações, sprites, capas e mockups sob demanda respeitando proporção (`9:16`, `1:1`, `16:9`) e estilo aprovado.
  - *Tier:* Modelo multimodal/imagem dedicado.

---

## 5. Vídeo & Edição Automática
- **Chefe de Edição** (`Advisor Audiovisual`, `avatarHue: 320`)
  - *Papel:* Planeja o vídeo ponta a ponta, define modo (`Gente`, `Motion` ou `Animado`), aprova pré-decupagem/mapa e coordena o time interno.
  - *Tier:* Alto (`high`).
- **Direção Criativa (Storyboard & Mapa)** (`Executor/Diretor`, `avatarHue: 280`)
  - *Papel:* Analisa o vídeo de referência e gera a decupagem por plano + `_CLAUDE/motion/mapa.json` alternando tela real, motion e B-roll.
  - *Tier:* Médio (`medium`).
- **Voz e Áudio** (`Executor Áudio`, `avatarHue: 30`)
  - *Papel:* Trata narração para WAV estéreo 48 kHz a `-14 LUFS`, gera transcrição com timestamps, ducking de trilha e seleção de SFX com licença.
  - *Tier:* Econômico (`medium` em Flash).
- **Edição e Motion** (`Executor Timeline`, `avatarHue: 320`)
  - *Papel:* Executa cortes, renderiza cenas HTML/GSAP (ex.: HyperFrames), sincroniza legendas SRT, monta FCP7 XML e gera preview MP4.
  - *Tier:* Médio/Alto (`high` em modelo de alto cache).
- **QA e Render** (`QA Independente`, `avatarHue: 100`)
  - *Papel:* Audita o vídeo com `ffprobe` (`1080×1920`, `60 fps`), mede loudness (`-14 LUFS`), confere sincronia de legendas, caminhos do XML e entrega pacote de publicação em `Docs/publicacao_redes.md`.
  - *Tier:* Econômico (`high` em Flash).

---

## 6. Web, Apps & Comercial *(Módulos Opcionais)*
- **Web & Sites:** `Tech Lead Web` (Advisor) → `Dev Frontend & UI` (Executor) + `QA, Performance & Deploy` (QA Lighthouse/Core Web Vitals).
- **Apps / SaaS:** `Product Owner` (Advisor) → `Tech Lead` (Arquiteto) → `Frontend` + `Backend` → `DevOps` + `QA Automatizado`.
- **Comercial & Prospecção:** `Advisor Comercial` → `Buscador de Leads` (Econômico/Free) → `Verificador de Dados` (Econômico/Free) → `Copywriter de Abordagem` (Econômico/Free).

---

## Modelo de Descrição Padrão para `create_agent`
Sempre inclua na `description` de cada agente criado:
1. Setor e papel exato (`Advisor`, `Executor` ou `QA Independente`).
2. Padrão de comunicação (*Zero Ping-Pong*: se completo, executar direto; se faltar dado bloqueante, listar todas as dúvidas de uma vez).
3. O que o agente **nunca** pode fazer sozinho (publicar, enviar mensagem a terceiros, pagar, sobrescrever originais).
4. Caminho absoluto do `ORGANOGRAMA_E_PROTOCOLO.md` compartilhado.
