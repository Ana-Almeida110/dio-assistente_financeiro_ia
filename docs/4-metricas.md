# Avaliação e Métricas

## Como Avaliar seu Agente

A avaliação do Finni pode ser feita de duas formas complementares:

1. **Testes estruturados:** Definindo perguntas e respostas esperadas com base nos dados mockados  
   (`transacoes.csv`, `categoria.json`, `usuarios.json`, `resumo_mensal.csv`, `alertas.json` e `limites_categoria.json`)
2. **Feedback real:** Pessoas testam o agente e avaliam a qualidade das respostas e a experiência de uso.

Essa abordagem permite verificar tanto a **precisão técnica** quanto a **utilidade prática** da solução.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | O agente respondeu corretamente com base nos dados disponíveis? | Perguntar o total gasto no mês e receber o valor correto |
| **Segurança** | O agente evitou inventar informações ou sair do escopo? | Perguntar algo fora do contexto e verificar se ele admite a limitação |
| **Coerência** | A resposta faz sentido dentro do contexto financeiro do usuário? | Informar que o limite de uma categoria foi ultrapassado quando os dados indicarem isso |
| **Proatividade** | O agente foi capaz de apresentar alertas ou orientações úteis? | Informar que o saldo está baixo ou que houve excesso de gastos em determinada categoria |
| **Clareza** | A resposta foi fácil de entender e útil para o usuário? | Avaliar se a explicação está simples, objetiva e bem estruturada |

---

## Exemplos de Cenários de Teste

Crie testes simples para validar seu agente:

### Teste 1: Consulta de gastos por categoria
- **Pergunta:** "Quanto gastei com alimentação?"
- **Resposta esperada:** Valor correspondente à soma das transações da categoria **Alimentação** no `transacoes.csv`
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 2: Registro de despesa
- **Ação:** Registrar uma nova despesa com descrição "Farmácia" no valor de R$ 45,00
- **Resultado esperado:** A despesa é registrada e categorizada corretamente como **Saúde**
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo
- **Pergunta:** "Qual a previsão do tempo?"
- **Resposta esperada:** O agente informa que é especializado apenas em controle financeiro pessoal
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 4: Informação inexistente
- **Pergunta:** "Qual foi meu gasto com academia em janeiro do ano passado?"
- **Resposta esperada:** O agente informa que não encontrou dados suficientes, caso essa informação não exista na base
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 5: Geração de alerta
- **Pergunta:** "Como estão meus gastos este mês?"
- **Resposta esperada:** O agente apresenta um resumo financeiro e, se aplicável, informa alertas como saldo baixo ou excesso de gastos
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 6: Consulta de limite restante por categoria
- **Pergunta:** "Quanto ainda posso gastar com saúde?"
- **Resposta esperada:** O agente calcula o valor restante com base em `limites_categoria.json` e nas transações registradas
- **Resultado:** [ ] Correto  [ ] Incorreto

---

## Resultados

Após os testes, registre suas conclusões:

**O que funcionou bem:**
- O agente conseguiu responder corretamente perguntas sobre saldo, gastos e categorias com base nos dados mockados;
- O uso de categorias, limites e alertas tornou as respostas mais úteis e contextualizadas;
- A linguagem simples e objetiva facilitou a interação com o usuário;
- A combinação entre regras de negócio e IA generativa aumentou a confiabilidade das respostas.

**O que pode melhorar:**
- Melhorar a interpretação de perguntas mais ambíguas ou formuladas de formas diferentes;
- Tornar a categorização automática mais precisa em descrições pouco específicas;
- Refinar os alertas para evitar mensagens repetitivas ou pouco relevantes;
- Evoluir a persistência de dados para uma solução mais robusta do que arquivos locais.

---

## Métricas Avançadas (Opcional)

Caso o projeto evolua, também podem ser observadas métricas técnicas como:

- **Latência:** tempo de resposta do agente;
- **Taxa de erro:** frequência de falhas ou respostas inválidas;
- **Uso de contexto:** quantidade de dados enviados ao modelo por interação;
- **Consistência:** se o agente mantém comportamento semelhante em perguntas equivalentes.

Como o projeto utiliza o **Ollama**, também é possível avaliar o desempenho local do modelo, considerando:

- velocidade de processamento;
- uso de memória;
- estabilidade em diferentes tipos de pergunta.
