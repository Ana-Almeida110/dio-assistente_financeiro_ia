# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `transacoes.csv` | CSV | Armazenar e analisar os gastos registrados pelos usuários |
| `categorias.json` | JSON | Classificar automaticamente os tipos de despesas com base em palavras-chave |
| `usuarios.json` | JSON | Armazenar dados básicos do usuário, como nome, saldo atual e limites mensal |
| `resumo_mensal.csv` | CSV | Apoiar análises e relatórios simples de gastos por período |
| `limites_categorias.json` | JSON | Definir limites de gastos por categoria de despesa |

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Os dados mockados foram adatados para simular um cenário real de **controle financeiro pessoal**.
Foram utilizados e/ou ajustados arquivos contendo informações como:
- Identificação do usuário;
- Saldo atual e limite mensal;
- Histórico de transações;
- Categorias de despesas;
- Alertas financeiros;
- Limites por categoria.

Além disso, o arquivo `categorias.json`foi estruturado para permitir a **classificação automática de despesas** com base em 
palavras-chave (ex.: "mercado" -> alimentação).
Também foi adicionado o arquivo `limites_categoria.json`, permitindo ao agente informar quanto o usuário ainda pode gastar em 
determinada categoria.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Os arquivos CSV e JSON são carregados pelo backend, principalmente a partir do arquivo `agente.py`, utilizando bibliotecas como **Pandas**, 
**JSON** e **OS**.

Esses dados são consultados sempre que o usuário:
- registra uma nova despesa;
- faz perguntas sobre seus gastos;
- solicita resumos financeiros;
- consulta alertas ou limites por categoria.

As transações podem ser atualizadas dinamicamente durante a execução da aplicação, permitindo que novas despesas registradas sejam incorporadas imediatamente à base de conhecimento. 

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

O backend consulta os arquivos conforme a necessidade e monta um **contexto personalizado** para o usuário selecionado. 
Esse contexto inclui, por exemplo:
- nome do usuário;
- saldo atual;
- limite mensal;
- total gasto no mês;
- gastos por categoria;
- últimas transações;
- alertas financeiros gerados.

Esse contexto é então enviado ao modelo local via **Ollama**, junto ao **system prompt**, para que o assistente gere respostas mais coerentes e contextualizadas.

Além disso, perguntas mais objetivas, como saldo atual ou total gasto por categoria, podem ser respondidas diretamente por regras de negócio, sem depender exclusivamente do modelo de linguagem.

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Você está atendendo o seguinte usuário:

- Nome: João - 
- Limite mensal: R$ 2.000,00

Total gasto no mês: R$ 689,00

Gastos por categoria:
- Alimentação: R$ 450,00
- Transporte: R$ 120,00
- Assinaturas: R$ 119,00

Últimas transações:
- 20/03: Supermercado - R$ 120 (Alimentação)
- 21/03: Uber - R$ 35 (Transporte)
- 22/03: Netflix - R$ 39 (Assinaturas)

Alertas:
- Você atingiu mais de 80% em Alimentação.
- Você excedeu o limite em Alimentação em R$ 100,00.

```

---

```markdown id="r7i2cx"
> **Observação:** A base de conhecimento do Finni foi projetada para ser simples, leve e adequada ao contexto acadêmico do projeto, utilizando arquivos locais em vez de banco de dados relacional. Essa escolha facilita testes, manutenção e entendimento da lógica do agente.

