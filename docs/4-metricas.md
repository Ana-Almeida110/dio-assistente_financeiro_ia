# Avaliação e Métricas

## Como Avaliar seu Agente

A avaliação pode ser feita de duas formas complementares:

1. **Testes estruturados:** Definindo perguntas e respostas esperadas com base nos dados mockados
   (`transacoes.csv`, `categorias.json`, `usuarios.json`, `resumo_mensal.csv` e `alertas.json`)
2. **Feedback real:** Pessoas testam o agente e avaliam a qualidade das respostas.

Essa abordagem permite verificar tanto a **precisão técnica** quanto a **experiência de uso**.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | O agente respondeu corretamente com base nos dados? | Perguntar o total gasto no mês e receber o valor correto|
| **Segurança** | O agente evitou inventar informações? | Perguntar algo fora do contexto e ele admitir que não sabe |
| **Coerência** | A resposta faz sentido dentro do contexto financeiro do usuário? | Alerta gasto excessivo quando a categoria ultrapassa o limite |
| **Proatividade** | O agente foi cpaz de sugerir alertas ou dicas úteis? | Informar que o saldo está baixo ou que houve excesso de gastos |

> [!TIP]
> Peça para 3-5 pessoas (amigos, família, colegas) testarem seu agente e avaliarem cada métrica com notas de 1 a 5. Isso torna suas métricas mais confiáveis! Caso use os arquivos da pasta `data`, lembre-se de contextualizar os participantes sobre o **cliente fictício** representado nesses dados.

---

## Exemplos de Cenários de Teste

Crie testes simples para validar seu agente:

### Teste 1: Consulta de gastos por categoria
- **Pergunta:** "Quanto gastei com alimentação?"
- **Resposta esperada:** Valor correspondente às transações da categoria alimentação no `transacoes.csv`
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 2: Registro de despesa
- **Pergunta:** "Gastei 45 reais com farmácia"
- **Resposta esperada:** O agente registra a despesa e a classifica corretamente (ex.: saúde)
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo
- **Pergunta:** "Qual a previsão do tempo?"
- **Resposta esperada:** Agente informa que é especializado em finanças
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 4: Informação inexistente
- **Pergunta:** "Qual foi meu gasto com academia em janeiro do ano passado?"
- **Resposta esperada:** O agente admite não ter dados suficientes, caso essa informação não exista na base
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 5: Geração de alerta
- **Pergunta:** "Como estão meus gastos este mês?"
- **Resposta esperada:** O agente apreenta um resumo e, se aplicável, informa alertas como saldo baixo ou gasto excessivo
- **Resultado:** [ ] Correto  [ ] Incorreto 

---

## Resultados

Após os testes, registre suas conclusões:

**O que funcionou bem:**
- O agente conseguiu responder corretamente perguntas sobre gastos e saldo com base nos dados mockados
- O uso de categorias e alertas tornou as respostas mais úteis e contextualizadas
- A linguagem simples facilitou a interação com o usuário

**O que pode melhorar:**
- Melhorar a interpretação de frases mais ambíguas do usuário
- Tornar a categorização automática mais precisa
- Refinar os alertas para evitar mensagens repetitivas ou pouco relevantes

---

## Métricas Avançadas (Opcional)

Caso o projeto evolua, também podem ser observadas métricas técnicas como:
- Latência: tempo de resposta do agente;
- Taxa de erro: frequência de fahas ou respostas inválidas;
- Uso de contexto: quantidade de dados enviados ao modelo por interação
- Consist~encia: se o agente mantém o mesmo comportamento em perguntas semelhantes

Como o projeto utiliza o **Ollama**, também é possível avaliar o desempenho local do modelo, considerando:
- velocidade de processamento
- uso de memória
- estabilidade em diferentes tipos de perguntas
