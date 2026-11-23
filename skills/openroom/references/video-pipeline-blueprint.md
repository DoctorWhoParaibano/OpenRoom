# Blueprint da Fábrica de Vídeos Automáticos & Clipes Virais (ex.: GTA 6)

Use este blueprint sempre que o usuário ativar o setor de **Vídeo & Edição** ou pedir pipelines automatizados de Reels, TikTok, Shorts e **clipes virais de GTA 6 / Games**.

---

## 1. Estrutura de Pastas Padronizada

```text
<VIDEO_ROOT>/                          # Ex.: C:\Users\<USER>\Videos ou ~/Videos
├── _BIBLIOTECA/
│   ├── references/                    # Vídeos de referência para análise de ritmo
│   ├── overlays/                      # Overlays, molduras, texturas locais
│   └── sfx/                           # Efeitos sonoros e trilhas licenciadas
├── _EQUIPE/
│   ├── perfis/                        # 1 arquivo por canal/marca (ex.: gta6-viral.md)
│   ├── templates/                     # briefing.md, roteiro.md, handoff.md
│   └── logs/
│       └── <AAAA-MM-DD_Projeto>/      # 00-briefing-pronto.md ... 06-qa.md
└── _ATIVOS/
    └── <perfil>/
        ├── _RADAR/
        │   └── <AAAA-MM-DD>/          # Clipes baixados + cortados 9:16 + pautas
        └── <AAAA-MM-DD_Projeto>/
            ├── Brutos/                # Originais (NUNCA editar ou apagar)
            ├── Docs/                  # briefing.md, roteiro.md, narracao_vNN.md, publicacao_redes.md
            ├── Assets/                # audio_tratado/, musica/, brand/, broll/
            ├── _CLAUDE/               # cortes/, motion/mapa.json, previews/, entregas/*.xml
            └── Renders/               # Versões finais aprovadas (_final_v01.mp4)
```

### Regras Inegociáveis de Arquivos
1. **Originais são somente leitura:** Nunca mover, renomear ou apagar arquivos em `Brutos/`.
2. **Versionamento sempre aditivo:** Nunca sobrescrever entregas (`_v01`, `_v02`, `_v03`…). Descartados vão para `_CLAUDE/_descartados/`.
3. **Arquivo é a verdade; chat é só aviso:** Toda mudança de etapa grava um handoff em `_EQUIPE/logs/<projeto>/NN-etapa-status.md`.

---

## 2. Os 3 Modos de Produção

| Aspecto | Modo A — Apresentador | Modo B — Motion (Sem Câmera) | Modo C — Clipes / Narrado / História |
|---|---|---|---|
| **Base visual** | Pessoa em câmera (`Brutos/camera`) | Tipografia, telas reais, gráficos HTML/GSAP | Clipes reais (ex.: GTA 6) + overlays + motion |
| **Áudio** | Lapela ou TTS/ElevenLabs | Narração tratada (`-14 LUFS`) + SFX | Narração + som original balanceado + SFX |
| **Ritmo alvo** | Cortes limpos no respiro + punch-ins | Troca visual a cada `1,2–1,8 s` | Gancho forte `0–3 s`, legendas e HUD dinâmico |
| **Saída técnica** | `1080×1920`, `60 fps`, XML + MP4 | `1080×1920`, `60 fps`, XML + MP4 | `1080×1920`, `60 fps`, XML + MP4 |

---

## 3. Pipeline em 7 Etapas (0 → 6)

1. **Etapa 0 — Briefing (`Chefe de Edição`):**
   - Cria a pasta do projeto e `Docs/briefing.md` definindo: perfil do canal, modo (`A`, `B` ou `C`), duração alvo, público, CTA, referência de ritmo e direitos.
2. **Etapa 1 — Roteiro & Narração (`Roteirista de Vídeo`):**
   - Pesquisa fatos verificáveis (tudo com fonte/URL; zero invenção) e gera `Docs/roteiro.md` em 5 blocos: **Gancho (0–3s) → Contexto/Dor → Desenvolvimento/Demo → Prova/Virada → CTA**, além de `Docs/narracao_v01.md`.
3. **Etapa 2 — Direção Criativa (`Direção Criativa`):**
   - Analisa vídeo de referência (cortes/segundo, curvas) e escreve a pré-decupagem plano a plano e depois o `_CLAUDE/motion/mapa.json` oficial após os cortes de áudio. Regra: nunca deixar duas telas estáticas seguidas; alternar `clipe/tela real ↔ motion ↔ b-roll`.
4. **Etapa 3 — Assets & Cenas (`Cenas e Imagens`):**
   - Captura prints reais, prepara clipes ou B-roll com resolução mínima `1080×1920` (ou crop sem distorção), registra origem e licença em `_CLAUDE/assets_escolhidos.md`.
5. **Etapa 4 — Voz & Áudio (`Voz e Áudio`):**
   - Trata narração para WAV estéreo `48 kHz` com loudness medido entre **`-14,5` e `-13,5 LUFS`** e pico `<= -1,5 dBFS` sem clipping; gera transcrição com timestamps por palavra/frase e seleciona trilha + SFX licenciados.
6. **Etapa 5 — Edição, Motion & Legendas (`Edição e Motion`):**
   - Monta os cortes pelo áudio tratado, renderiza cenas animadas (HTML/CSS/GSAP via HyperFrames ou FFmpeg), sincroniza legendas dinâmicas e exporta XML + preview MP4 (`_CLAUDE/previews/`).
7. **Etapa 6 — QA Técnico & Pacote de Redes (`QA e Render`):**
   - Valida com `ffprobe` (`1080×1920`, `60 fps`, streams de vídeo e áudio), confirma `-14 LUFS`, checa ortografia/sincronia das legendas e gera `Docs/publicacao_redes.md` (título, legenda, gancho e hashtags para TikTok, Reels e YouTube Shorts).
   - **Publicação:** Apenas o usuário aprova e publica.

---

## 4. Automação Especial: Clipes Virais & Notícias de GTA 6

Para montar uma linha automática de **clipes virais / notícias de jogos (ex.: GTA 6)**:

### Passo 1 — Perfil do Canal (`_EQUIPE/perfis/gta6-viral.md`)
Defina no perfil: estilo editorial, paleta de cores, fonte das legendas, tamanho alvo (`30–55s`), fontes oficiais permitidas (ex.: canais oficiais da publisher, portais verificados, streams/clipes creditados) e formatos permitidos.

### Passo 2 — Rotina Agendada do `Radar Viral` (`openbot.create_routine`)
Configure uma rotina recorrente (ex.: diariamente às `08:00` e `18:00`):
- **Coleta:** Buscar novidades verificadas de GTA VI / trailers / análises de frame / vazamentos confirmados vs. rumores marcados claramente como rumor, ou clipes de alta retenção com URL e autor.
- **Corte automático 9:16 (`yt-dlp` + `ffmpeg`):**
  ```bash
  # Exemplo de corte vertical 1080x1920 a 60fps com centralização segura
  ffmpeg -y -ss <INICIO> -t <DURACAO> -i "<CLIP_ORIGEM>" \
    -vf "scale=1080:1920:force_original_aspect_ratio=increase,crop=1080:1920,fps=60" \
    -c:v libx264 -preset medium -crf 18 -c:a aac -ar 48000 -b:a 192k \
    "<VIDEO_ROOT>/_ATIVOS/gta6-viral/_RADAR/<DATA>/clip_01.mp4"
  ```
- **Classificação obrigatória:**
  - **`Clipe + Motion`**: clipe impactante pronto para ganhar legenda cinética, zoom de ênfase, barra de contexto no topo e SFX.
  - **`Roteiro + Motion`**: notícia/curiosidade que exige narração rápida (`~150 palavras/min`), B-rolls alternados e cards de evidência na tela.
- **Silêncio inteligente:** Se nada novo/relevante surgiu desde a última checagem, o Radar chama `routine_no_update` para não gerar ruído nem gastar cota à toa.

### Passo 3 — Encadeamento Automático (`openbot.connect_routine_agents`)
Ligue a rotina do **Radar Viral** diretamente ao **Chefe de Edição** (`fromAgentId = Radar`, `toAgentId = Chefe de Edição`). Assim que o Radar entrega o pacote com os clipes em `_RADAR/<DATA>/`, o Chefe de Edição avalia o gancho `0–3 s`, abre o projeto em `_ATIVOS/gta6-viral/<DATA>_<Tema>/` e dispara o pipeline até o preview pronto para sua aprovação.
