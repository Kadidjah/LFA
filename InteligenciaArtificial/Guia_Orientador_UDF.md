# Orientador UDF: sistema especialista de optativas

**Inteligência Artificial · Profa. Kadidja Valéria**

O Orientador UDF verifica se o perfil informado atende aos critérios de uma optativa escolhida pelo estudante. É um protótipo didático: nomes e critérios são fictícios e não representam a oferta, os pré-requisitos ou as regras de matrícula da UDF.

## 1. Execute o exemplo

1. Salve `orientador_udf.py` em uma pasta.
2. Abra o terminal nessa pasta e execute `python orientador_udf.py` (ou `python3 orientador_udf.py`). Use Python 3; não é preciso instalar bibliotecas. No Colab, cole todo o código em uma célula e execute.
3. Escolha **1 — Introdução à IA**. Responda **s** às duas perguntas. Confira se o sistema recomenda a optativa e identifica a regra R1.
4. Repita com **n** na primeira pergunta. Confira se a regra é rejeitada e se o programa encerra a investigação sem fazer a segunda pergunta.
5. Repita com **?** na primeira e **s** na segunda. Confira se o sistema informa que faltam dados.

## 2. Identifique fatos, regras e objetivo

Os três fatos são o interesse por **matemática**, **programação** e **análise de dados**. Cada um pode ser verdadeiro, falso ou não informado. Em uma consulta de exemplo, os fatos podem ser: matemática = sim, programação = sim, dados = não.

| Regra | SE | ENTÃO |
|---|---|---|
| R1 | Gosta de matemática e de programação | Recomendar Introdução à IA |
| R2 | Gosta de analisar dados e de matemática | Recomendar Análise de Dados |
| R3 | Gosta de programação e não gosta de analisar dados | Recomendar Desenvolvimento de Software |
| R4 | Gosta de analisar dados e não gosta de matemática | Recomendar Visualização de Dados |
| R5 | Gosta de matemática e não gosta de programação | Recomendar Fundamentos de Lógica |

**Base de conhecimento:** `REGRAS`. **Memória de trabalho:** dicionário `fatos`. **Motor de inferência:** função `consultar`. **Interface:** funções `main` e `perguntar_console`. O rastro é a explicação de quais premissas foram verificadas e quais valores o sistema encontrou.

## 3. Simule o encadeamento para trás

A pergunta inicial é **“Os critérios para recomendar Introdução à IA estão satisfeitos?”**. O motor procura a regra cuja conclusão é essa recomendação: R1.

| Passo | Verificação | Resultado no exemplo |
|---|---|---|
| 1 | O fato “gosta de matemática” já está na memória? | Se não estiver, pergunta. Resposta: sim. |
| 2 | O fato “gosta de programação” já está na memória? | Se não estiver, pergunta. Resposta: sim. |
| 3 | As duas premissas de R1 foram confirmadas? | Sim. Recomenda Introdução à IA e explica a decisão. |

A pergunta sobre análise de dados não é necessária para R1. O exemplo usa **encadeamento para trás em um nível**: parte da conclusão desejada e busca fatos que a sustentem. Há uma regra por optativa; o protótipo não procura todas as recomendações nem encadeia subobjetivos. Uma premissa incompatível impede confirmar a regra; uma premissa desconhecida, sem incompatibilidades, torna a resposta inconclusiva.

## 4. Atividade: desenvolva seu próprio sistema especialista

1. **Delimite o domínio.** Escolha, por exemplo, orientação para uma trilha de estudos ou triagem de problemas de laboratório. Escreva quem consulta o sistema, qual decisão ele apoia e quais casos ficam fora do escopo.
2. **Defina três fatos observáveis.** Escreva uma pergunta por fato e explique o significado de sim, não e não informado.
3. **Modele cinco regras SE–ENTÃO.** Numere-as, defina seus objetivos e explique de onde vieram os critérios: material consultado, entrevista ou hipótese didática explícita. Para reaproveitar o motor do exemplo, mantenha uma regra por objetivo.
4. **Simule antes de programar.** Escolha um objetivo, encontre a regra correspondente e registre a ordem das perguntas que seriam feitas. Faça uma simulação confirmada e outra inconclusiva.
5. **Implemente.** Adapte `PERGUNTAS` e `REGRAS`, mantendo a base de conhecimento separada do motor. Mostre o objetivo, o resultado e a justificativa. Não transforme ausência de resposta em “não”.
6. **Teste.** Registre os fatos, o resultado esperado, o resultado obtido e a regra verificada em cada cenário. Teste também cada uma das cinco regras ao menos uma vez.
7. **Demonstre.** Apresente uma consulta completa e outra sem informação suficiente. Explique uma limitação e proponha uma melhoria.

| Teste de referência | Entrada | Resultado esperado |
|---|---|---|
| Confirmação de R1 | Matemática: sim; programação: sim | Recomenda Introdução à IA |
| Premissa falsa | Matemática: não | Critério não atendido; programação não precisa ser perguntada |
| Premissa desconhecida | Matemática: ?; programação: sim | Informação insuficiente |
| Premissa negativa de R3 | Programação: sim; dados: não | Recomenda Desenvolvimento de Software |
| Entrada inválida | Digitar algo diferente de s, n ou ? | Solicita resposta válida |

**Entregáveis:** código executável, README com escopo e instruções de execução, tabela das cinco regras, uma simulação de encadeamento para trás e registro dos testes. A correção observa a coerência das regras, a separação entre base e motor, o tratamento de informações ausentes e a qualidade das explicações.

**Material-base:** *Sistemas Especialistas*, PDF fornecido para a aula, slide “Hands On! Modelando o seu Sistema”.
