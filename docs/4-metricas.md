# Avaliação e Métricas

## Como Avaliar seu Agente

A avaliação do **Finni** deve considerar dois aspectos principais:
1. **Precisão funcional**, verificando se o sistema responde corretamente com base nos dados disponíveis;   
2. **Qualidade da experiência**, analisando se as respostas são úteis, claras, coerentes e seguras para o usuário.

Como o projeto combina **regras de negócio determinísticas** com **IA generativa local (Ollama)**, a avaliação deve observar tanto o comportamento
do código quanto a qualidade das respostas produzidas pelo modelo.

A validação pode ser feita de duas formas complementares:
1. **Testes estruturados**
São testes com entradas definids e respostas esperadas, baseadas nos arquivos da aplicação:
- `transacoes.csv`
- `usuarios.json`
- `categoria.json`
- `limites_categoria.json`

Esses testes permitem validar se:
- os cálculos estão corretos;
- as categorias estão sendo reconhecidas corretamente;
- os alertas estão funcionando;
- as respostas objetivas estão consistentes.

  2. **Testes de uso real**
  Consistem em interações livres com o sistema, feitas por usuários ou avaliadores, para observar:
- clareza das respostas;
- naturalidade da conversa;
- utilidade das orientações;
- robustez diante de perguntas ambíguas ou inesperadas.
Essa abordagem permite avaliar o Finni do ponto de vista técnico, prática e experiencial.

---

## Estratégia de Avaliação
O Finni possui um **fluxo híbrido de resposta**, que exige uma avaliação dividida em duas camadas:

**Respostas determinísticas (Python)**
São respostas geradas diretamente pelas regras implementadas no backend, sem uso do modelo de linguagem.

Exemplos:
- "Quanto gastei com alimentação?"
- "Quanto ainda posso gastar com saúde?"
- "Quais são minhas últimas transações?"

Nesses casos, a avaliação deve focar em:
- exatidão dos cálculos;
- consistência lógica;
- aderência aos dados.

## Respostas abertas (IA local)
São respostas geradas com apoio do **Ollama**, utilizadas quando a pergunta exige interpretação, explicação ou orientação mais livre.

Exemplos:
- "Como posso economizar em alimentação?"
- "Como estão meus hábitos de gasto?"
- "O que posso melhorar nas minhas finanças?"

Nesses casos, a avaliação deve focar em:
- clareza;
- coerência com o contexto;
- utilidade prática;
- ausência de informações inventadas.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | Se a resposta está correta com base nos dados disponíveis | Consultar o total gasto em uma categoria e comparar com o valor real no `transacoes.csv` |
| **Segurança** | Se o agente evita inventar informações ou sair do escopo financeiro | Perguntar algo sem relação com finanças e verificar se ele reconhece a limitação |
| **Coerência Contextual** | Se a resposta faz sentido dentro do histórico e do orçamento do usuário | Informar corretamente quando um limite foi ultrapassado |
| **Clareza** | Se a resposta é compreensível, objetiva e útil | Avaliar se a linguagem está simples e fácil de interpretar |
| **Consistência** | Se perguntas equivalentes geram respostas equivalentes | Fazer a mesma pergunta com variações de escrita e comparar o comportamento |
| **Robustez** | Se o sistema lida bem com perguntas ambíguas, incompletas ou inesperadas | Testar frases como "quanto tenho ainda?" ou "como estão meus gastos?" |
| **Proatividade** | Se o agente oferece alertas e orientações úteis quando apropriado | Informar excesso de gastos ou proximidade do limite da categoria |
| **Qualidade da IA** | Se respostas abertas geradas pelo modelo são relevantes e contextualizadas | Pedir dicas de economia e avaliar se a resposta é prática e coerente |

---

## Exemplos de Cenários de Teste

Crie testes simples para validar seu agente:

### Teste 1: Consulta de gastos por categoria
- **Pergunta:** "Quanto gastei com alimentação?"
- **Resposta esperada:** Valor correspondente à soma das transações da categoria **Alimentação** 
- **Resultado:** [X] Correto  [ ] Incorreto

### Teste 2: Registro de despesa
- **Ação:** Registrar uma nova despesa com descrição "Farmácia" 
- **Resultado esperado:** A despesa é registrada e categorizada corretamente como **Saúde**
- **Resultado:** [X] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo
- **Pergunta:** "Qual a previsão do tempo?"
- **Resposta esperada:** O agente informa que é especializado apenas em controle financeiro pessoal
- **Resultado:** [X] Correto  [ ] Incorreto

### Teste 4: Geração de alerta
- **Pergunta:** "Como estão meus gastos este mês?"
- **Resposta esperada:** O agente apresenta um resumo financeiro e, se aplicável, informa alertas como saldo baixo ou excesso de gastos
- **Resultado:** [X] Correto  [ ] Incorreto

### Teste 5: Consulta de limite restante por categoria
- **Pergunta:** "Quanto ainda posso gastar com saúde?"
- **Resposta esperada:** O agente calcula o valor restante com base em `limites_categoria.json` e nas transações registradas
- **Resultado:** [X] Correto  [ ] Incorreto

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


