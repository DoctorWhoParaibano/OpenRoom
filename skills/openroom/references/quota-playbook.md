# Playbook de Cotas, Modelos e Fallbacks — OpenRoom

Use estas regras ao configurar `model`, `reasoningEffort`, `providerAccountId` e `backupModels` em todos os agentes.

---

## 1. Por que estruturas multi-agente queimam cota rápido
1. **Esforço `xhigh` ligado por padrão:** Gera cadeias enormes de raciocínio em tarefas rotineiras e multiplica o consumo de saída/entrada.
2. **Modelo pesado em executor de volume:** Colocar modelo topo de linha em agente que lê logs, faz scraping, limpa listas ou roda cron diário drena a janela de horas em poucos turnos.
3. **Acúmulo em uma única conta:** Deixar 10+ agentes na conta `default` enquanto outras contas conectadas ficam com 1–2 agentes estoura o limite de uma conta antes mesmo de usar as outras.
4. **Loop de fallback na mesma conta:** Quando o primeiro backup do agente usa o mesmo `providerAccountId` do modelo principal, uma queda de cota da conta trava em cascata.

---

## 2. Regras de Ouro de Configuração

### Regra A — Níveis de Esforço (`reasoningEffort`)
- **`xhigh`:** **Nunca** usar como padrão em nenhum agente. Ative só manualmente para auditorias pontuais ou bugs críticos.
- **`high`:** Apenas para **Advisors**, arquitetos de software, direção de arte/UI e motion complexo.
- **`medium`:** Ideal para builders de frontend/copy, decupagem criativa, triagem e geração visual.
- **`low` (ou Flash `medium`/`high`):** Ideal para executores operacionais, pesquisa, radares agendados, verificação de dados e QA repetitivo.

### Regra B — Matriz de Classes de Modelo (adaptável ao seu `openbot.list_models`)
Sempre mapeie os modelos reais disponíveis em `openbot.list_models` para 4 classes:

| Classe | Quando usar | Exemplos típicos de papel |
|---|---|---|
| **Classe S (Arquitetura & UI)** | Apenas onde layout estruturado, código multi-arquivo ou UI complexa exigem máxima precisão | `Tech Lead`, `Direção de Arte & UI` |
| **Classe A (Estratégia & Direção)** | Orquestração, roteiro estratégico, direção criativa e edição complexa com bom cache | `Supervisor`, `Gerente`, `Chefe de Edição`, `Edição e Motion` |
| **Classe B (Rápido / Flash)** | Pesquisa, áudio, revisão editorial/QA, roteiros curtos, triagem e radares diários | `Briefing`, `Roteirista`, `Voz e Áudio`, `QA`, `Radar Viral` |
| **Classe F (Gratuito / OpenCode Free / Local)** | Tarefas de alto volume de leitura/execução, devops/testes rotineiros, captação e limpeza de leads | `Operações`, `Buscador de Leads`, `Verificador`, `QA Automatizado` |

*(Se um modelo com cota semanal/limitada esgotar em todas as contas, mova seus agentes para a Classe A estável e remova o modelo esgotado tanto do primário quanto da cadeia de `backupModels`.)*

### Regra C — Distribuição Balanceada entre Contas
Suponha $N$ agentes usando o provedor principal com $K$ contas conectadas (`account_1`, `account_2`, ..., `account_K`):
- Distribua cerca de $\lceil N / K \rceil$ agentes por conta.
- Misture agentes pesados e leves em cada conta (nunca junte todos os Advisors na mesma conta).

### Regra D — Cadeia de Fallback Segura (`automatic: true`)
Todo agente deve ter `backupModels.automatic = true` e uma escada de 3 a 4 degraus:
1. **Salto 1:** Mesmo nível (ou nível imediatamente abaixo) em **outra conta** (`providerAccountId` obrigatoriamente diferente do principal).
2. **Salto 2:** Modelo rápido/estável em uma **terceira conta** (se existir).
3. **Salto 3:** **Provedor alternativo** (ex.: Codex, OpenRouter, custom endpoint ou modelo gratuito).
4. **Salto 4 (rede de segurança final):** Modelo gratuito (ex.: `opencode/...-free`), garantindo que um pipeline não morra no meio por falta de cota.

---

## 3. Auditoria Pós-Configuração
Ao terminar o provisionamento (ou periodicamente pelo Supervisor), confira sempre:
- `0` agentes com `reasoningEffort === "xhigh"` como padrão;
- `0` agentes com `backupModels.automatic !== true`;
- `0` agentes cujo 1º backup usa o mesmo `providerAccountId` do principal;
- `0` modelos que o usuário pediu para evitar (ou que já estejam esgotados);
- `0` agentes presos em estado de retorno com erro (`usageLimitReturn`).
