# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `transacoes.csv` | CSV | Armazenar e analisar os gastos do usuário |
| `categorias.json` | JSON | Classificar automaticamente os tipos de despesas |
| `usuarios.json` | JSON | Armazenar dados básicos do usuário |
| `resumo_mensal.csv` | CSV | Gerar relatórios simples de gastos por períodos |
| `alertas.csv` | JSON | Definir regras e mensagens de alertas financeiros |

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Os dados mockados foram adatados para simular um cenário real de controle financeiro pessoal.
Foram incluídos campos como:
- Data de transação
- Descrição do gasto
- Valor
- Categoria

Além disso, o arquivo `categorias.json`foi estruturado para permitir a **classificação automática de despesas** com base em 
palavras-chave (ex.: "mercado" -> alimentação).

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Os arquivos CSV e JSON são carregados pelo backend no início da execução do sistema.
Os dados podem ser:
- Mantidos em memória durante a sessão
- Atualizados conforme o usuário registra novos gastos

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Os dados são utilizados de forma **dinâmica**, ou seja:
- O backend consulta os arquivos conforme a necessidade
- Apenas os dados relevantes são enviados para o modelo
- As informações são incluídas no contexto do prompt antes da geração da resposta
Isso evita sobrecarga e melhora a precisão das respostas

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Dados do Usuári9:
- Nome: João 
- Saldo atual: R$ 1.250

Últimas transações:
- 20/03: Supermercado - R$ 120 (Alimentação)
- 21/03: Uber - R$ 35 (Transporte)
- 22/03: Netflix - R$ 39 (Assinaturas)

Resumo do mês:
- Alimentação: R$ 450
- Transporte: R$ 120
- Assinaturas: R$ 80

```
