# Tutorial Completo — Montando seu OpenRoom no OpenBot

Este guia mostra como sair de um OpenBot recém-instalado para uma equipe multi-agente estruturada, econômica em cotas e pronta para rodar fluxos automáticos (incluindo produção de vídeos curtos e clipes virais de **GTA 6**).

---

## 1. Pré-requisitos

### Obrigatórios (para qualquer estrutura)
- **OpenBot** instalado e rodando no seu computador.
- Pelo menos **1 provedor conectado** nas configurações do OpenBot (ex.: contas Google/Antigravity, Codex, OpenCode Free ou gateway compatível com OpenAI).
- **Recomendado:** 2 ou mais contas conectadas ou um provedor gratuito/leve secundário para permitir **rotação de cotas** e **fallback automático** sem travar os agentes.

### Opcionais (para a Fábrica de Vídeos & Clipes Virais)
Se você quiser ativar o setor de **Vídeo & Edição** e o **Radar Viral (ex.: GTA 6)**:
- **FFmpeg** e **FFprobe** no `PATH` do sistema (cortes, loudness `-14 LUFS`, validação de render).
- **yt-dlp** (download de referências e clipes públicos autorizados).
- **Python 3.10+** e **Node.js 20+** (automação de scripts, transcrição local como Whisper/WhisperX e cenas HTML/CSS/GSAP com **HyperFrames**).

---

## 2. Instalando a Skill `openroom`

Você tem duas formas simples de instalar:

### Opção A — Pedir ao próprio agente principal para importar
1. Baixe ou clone este repositório dentro de uma pasta acessível ao seu agente (ou na pasta `Shared` do OpenBot):
   ```bash
   git clone https://github.com/DoctorWhoParaibano/OpenRoom.git
   ```
2. Copie a pasta `OpenRoom/skills/openroom` para dentro do workspace do seu agente principal (ou para `~/.agents/skills/openroom`).
3. No chat do seu agente principal, diga:
   > *"Registre a skill local que está na pasta `skills/openroom` e use-a agora para configurar minha estrutura no OpenBot."*

### Opção B — Colar diretamente como skill local
Se você já tem acesso às configurações de Skills do OpenBot, importe a pasta `skills/openroom/` (que já contém o `SKILL.md` e os manuais em `references/`) na biblioteca local e ative-a no seu agente principal (**Supervisor** ou equivalente).

---

## 3. Como funciona a Entrevista Guiada

Ao acionar a skill `openroom`, o agente **não sai criando 30 bots aleatórios**. Ele segue 5 fases controladas:

1. **Descoberta silenciosa:** Lê seus provedores, modelos e contas já conectadas no OpenBot e checa quais agentes ou skills já existem.
2. **Rodada 1 — Negócio & Setores (2 a 3 perguntas):** Pergunta o nome do seu projeto/estúdio, idioma e quais módulos você quer ligar agora (ex.: Vídeo & Clipes, Web/Landing Pages, Comercial, Conteúdo).
3. **Rodada 2 — Política de Cotas & Modelos (2 a 3 perguntas):** Mostra quantas contas/provedores você tem disponíveis e pergunta se você prefere **Economia Máxima**, **Equilíbrio (Recomendado)** ou **Máxima Qualidade**, além de confirmar uso de modelos gratuitos no volume.
4. **Rodada 3 — Automações & Pastas (2 a 3 perguntas):** Define a pasta compartilhada raiz (ex.: `~/OpenBot/Shared`), a pasta de vídeos (`~/Videos/_EQUIPE`), canais/nichos de radar (como **GTA 6**, tecnologia, curiosidades) e horários de execução automática.
5. **Aprovação & Provisionamento:** Apresenta uma tabela completa com cada agente, modelo, esforço de raciocínio, cadeia de fallback e rotinas. Só cria depois do seu **OK**.

---

## 4. Organizando os Setores na Barra Lateral (Sidebar)

No OpenBot, você pode agrupar agentes por **Seções** na barra lateral para que cada líder priorize colegas do próprio setor:

| Seção Sugerida | Função | Agentes típicos |
|---|---|---|
| **Diretoria & Operações** | Comando, triagem e revisão final | `Supervisor`, `Gerente`, `Operações`, `QA Editorial` |
| **Pesquisa & Inteligência** | Dossiês, validação e radares | `Briefing & Pesquisa`, `Radar Viral (ex.: GTA 6)` |
| **Copy & Roteiro** | Textos, roteiros e prospecção | `Roteirista de Vídeo`, `Copy & Estrutura Web`, `Conteúdo` |
| **Criativos & Design** | Direção de arte, assets e thumbs | `Direção de Arte & UI`, `Cenas e B-Roll`, `Gerador de Imagens` |
| **Vídeo & Edição** | Fábrica audiovisual completa | `Chefe de Edição`, `Direção Criativa`, `Voz e Áudio`, `Edição e Motion`, `QA e Render` |
| **Web & Apps** *(opcional)* | Sites e software | `Tech Lead`, `Dev Frontend`, `Dev Backend`, `QA & Deploy` |

> **Dica de ouro:** Mantenha apenas **1 a 2 líderes (Advisors)** por frente. Um bom Advisor escreve **1 pedido autocontido** com caminhos absolutos, entradas, formato de saída e critério de aceite — evitando "ping-pong" de mensagens que queima cota.

---

## 5. Configurando Cotas e Fallbacks sem Quebrar

O maior erro de quem cria vários agentes é deixar todos no modelo mais caro com esforço máximo (`xhigh`). No OpenRoom:

1. **Nunca use `xhigh` como padrão.** Use `high` apenas em Advisors, arquitetos e direção criativa; use `medium` em execução de código/copy; use `low` ou modelos gratuitos/Flash em triagem, busca e rotinas de volume.
2. **Ative `fallback` automático (`automatic: true`) em todos os agentes.**
3. **Regra da conta cruzada:** Se um agente usa a `Conta A` como principal, o **primeiro fallback dele nunca pode ser a `Conta A`**. Deve apontar para a `Conta B` (ou outro provedor), depois `Conta C`, e por último um modelo econômico/gratuito.
4. **Espalhe os agentes pelas contas:** Se você tem 4 ou 5 contas conectadas e 20 agentes, coloque ~4–5 agentes em cada conta em vez de acumular 12 na conta padrão.

---

## 6. Configurando a Fábrica Automática de Vídeos & Clipes de GTA 6

Se você ativar o módulo de vídeo no OpenRoom, ele cria uma esteira previsível com separação total entre **originais**, **arquivos gerados** e **entregas**:

```text
~/Videos/
├── _BIBLIOTECA/
│   ├── references/        # Vídeos de referência baixados para medir ritmo e cortes
│   └── overlays/          # Overlays, molduras e pacotes locais
├── _EQUIPE/
│   ├── perfis/            # Regras de cada canal (ex.: gta6-shorts.md)
│   ├── templates/         # Modelos de briefing e roteiro
│   └── logs/              # Handoffs por projeto (01-roteiro-pronto.md, etc.)
└── _ATIVOS/
    └── <perfil>/
        ├── _RADAR/AAAA-MM-DD/       # Clipes e pautas capturados automaticamente
        └── AAAA-MM-DD_NomeProjeto/
            ├── Brutos/              # Originais (somente leitura)
            ├── Docs/                # briefing.md, roteiro.md, publicacao_redes.md
            ├── Assets/              # B-roll, telas reais, áudio tratado (-14 LUFS)
            ├── _CLAUDE/             # Cortes JSON, mapa de motion, previews MP4, XML
            └── Renders/             # Vídeo final aprovado (_v01, _v02...)
```

### Fluxo automático para Clipes de GTA 6 (exemplo real da arquitetura)
1. **Radar Viral (Rotina Diária):** Todo dia em horário configurado (ex.: `08:00` e `18:00`), o agente **Radar Viral** busca notícias verificadas sobre GTA VI, trailers, análises de mapa/mecânicas e clipes em alta com URL fonte.
2. **Corte e Classificação Automática:** Baixa o trecho com `yt-dlp`, recorta para vertical `9:16` (`1080×1920`) com `ffmpeg` na pasta `_RADAR/AAAA-MM-DD/` e classifica o gancho nos primeiros 3 segundos em:
   - **`Clipe + Motion`:** quando o vídeo em si já segura a atenção (legenda dinâmica + zoom/HUD + SFX).
   - **`Roteiro + Motion`:** quando precisa de narração explicativa com cortes rápidos a cada `1,2–1,8 s`.
3. **Encadeamento Automático (`connect_routine_agents`):** O OpenBot envia automaticamente o pacote do Radar para o **Chefe de Edição**, que aciona **Roteirista** → **Direção Criativa** → **Cenas/Áudio (`-14 LUFS`)** → **Edição e Motion** → **QA e Render**.
4. **Gate Humano:** Nenhum agente publica ou apaga vídeos automaticamente sem a sua aprovação final.

---

## 7. Operação no Dia a Dia (Boas Práticas)

- **Peça sempre ao líder da frente:** Quer um vídeo? Fale com o `Chefe de Edição` ou `Gerente`, não microgerencie 5 agentes manualmente.
- **Exija evidência no QA:** O agente de QA nunca deve dizer "ficou ótimo" de boca — ele precisa rodar `ffprobe`, conferir loudness (`-14 LUFS`), verificar links/mobile ou rodar a suíte de testes antes de aprovar.
- **Revise cotas semanalmente:** Peça ao seu `Supervisor` para auditar quais agentes estão consumindo mais tokens e redistribuir contas ou baixar esforços de raciocínio quando necessário.
