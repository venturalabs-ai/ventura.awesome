# Skill: ventura.awesome — LOOP Skill Engine / Deterministic Replay

Skill de curadoria e recomendação de recursos com **execução determinística**:
explore a necessidade uma vez, compile o índice, replique a recomendação com
~zero tokens, regenere quando um recurso envelhecer.

## Trigger

Use quando o usuário quiser: achar recurso/ferramenta/curso para uma
necessidade, comparar opções, montar lista de referências, descobrir boas
práticas, saber "o que a comunidade recomenda".

## Arquitetura Token-Efficient & Regenerative

| Fase | Descrição | Consumo |
|---|---|---|
| **Explore** | Modelo forte analisa necessidade + categorias curadas (uma vez) | Alto (único) |
| **Compile** | Gera `indice.md`: categoria, recurso, uso, por que escolher | Baixo |
| **Replay** | Recomenda recurso pela necessidade — sem reavaliar tudo | Mínimo/Zero |
| **Regenerate** | Recurso desatualizado/superado → regenere a seleção | Sob demanda |

## Receita determinística (Replay)

```text
1. PEDIDO   — "recurso para X" | "alternativa a Y" | "melhor em Z"
2. RECEITA  — consulta indice.md: categoria, recurso, uso, critério
3. EXECUTA  — 1. mapeia necessidade para categoria | 2. seleciona recurso
             3. entrega com uso prático e alternativa
4. REGISTRA — recurso usado, avaliação, contexto
5. STOP-YIELD — recurso não atende (custo/manutenção) → sinaliza regenerar
```

## Regras de engenharia

- **Token Budget** — Explore: até 4k tokens. Replay: < 200 tokens.
- **Context Firewall** — o replay só vê o índice compilado (nunca a lista inteira).
- **Prefix Caching** — o sistema deste arquivo fica byte-stable.
- **Skill Distillation** — recomendação validada vira índice permanente.
- **Regeneração** — recurso caiu em desuso → volta ao Explore.

## Como compilar o índice (Explore → Compile)

```text
1. Levanta a necessidade e o escopo (aprender/ferramenta/carreira)
2. Aplica os critérios: útil, mantido, acessível, testado
3. Compila indice.md por categoria com 3-5 recursos fortes cada
4. Valida com o usuário e ativa o Replay
```

## Exemplo de uso

```text
Atue como ventura.awesome (modo REPLAY). Meu indice.md diz: "Frontend —
componentes de UI". Recomende o recurso certo para montar um design system
enxuto. Use menos de 200 tokens e registre o uso.
```
