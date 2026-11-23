# Organograma e Protocolo Operacional — <NOME_DA_OPERACAO>

Este documento é a referência oficial de setores, donos, fluxo entre agentes e regras de qualidade do workspace **<NOME_DA_OPERACAO>**.

---

## 1. Estrutura de Setores e Agentes

| Setor | Agente | Papel (`Advisor` / `Executor` / `QA`) | Modelo / Conta |
|---|---|---|---|
| Diretoria & Operações | Supervisor | Advisor Infra & Cotas | `<provider>/<model>` |
| Diretoria & Operações | Gerente | Advisor Orquestrador | `<provider>/<model>` |
| Pesquisa & Inteligência | Briefing & Pesquisa | Executor | `<provider>/<model>` |
| Pesquisa & Inteligência | Radar Viral | Executor Agendado | `<provider>/<model>` |
| Copy & Roteiro | Roteirista de Vídeo | Executor | `<provider>/<model>` |
| Criativos & Design | Direção de Arte & UI | Advisor Criativo | `<provider>/<model>` |
| Criativos & Design | Cenas e Imagens | Executor | `<provider>/<model>` |
| Vídeo & Edição | Chefe de Edição | Advisor Audiovisual | `<provider>/<model>` |
| Vídeo & Edição | Direção Criativa | Executor / Direção | `<provider>/<model>` |
| Vídeo & Edição | Voz e Áudio | Executor Áudio | `<provider>/<model>` |
| Vídeo & Edição | Edição e Motion | Executor Timeline | `<provider>/<model>` |
| Vídeo & Edição | QA e Render | QA Independente | `<provider>/<model>` |

*(Adicione ou remova linhas conforme os módulos ativados na entrevista.)*

---

## 2. Protocolo de Comunicação (Zero Ping-Pong)

1. **Advisors enviam 1 pedido autocontido** contendo:
   - Projeto / Marca / Perfil (nunca misturar projetos diferentes);
   - Objetivo e plano passo a passo;
   - Caminhos absolutos dos arquivos de entrada;
   - Local exato de saída e critério objetivo de aceite;
   - Limites (o que não pode alterar/publicar/excluir).
2. **Executores respondem em 1 entrega completa:**
   - Se os dados estiverem completos: executam sem perguntas desnecessárias e devolvem **Status + Caminhos absolutos + Evidência checada + Próximo passo**.
   - Se faltar informação bloqueante: param e listam **todas** as dúvidas de uma vez, sem chutar fatos.
3. **Arquivo é a verdade:** Nenhuma entrega existe só no chat. Todo arquivo gerado é salvo na pasta do projeto e registrado no log de handoff.

---

## 3. Portões de Qualidade (Gates) e Segurança

- **Zero invenção:** Toda informação factual sem fonte confirmada deve ser marcada como `a confirmar`.
- **QA independente obrigatório:** Quem produz não aprova a própria entrega. Vídeo passa por conferência técnica (`ffprobe` + loudness `-14 LUFS`); site/app passa por build, testes e checagem visual antes de deploy.
- **Aprovação humana obrigatória antes de:**
  - Publicar vídeos, posts ou sites em produção;
  - Enviar mensagens externas para clientes/leads;
  - Apagar arquivos originais ou gastar saldo/serviços pagos.
