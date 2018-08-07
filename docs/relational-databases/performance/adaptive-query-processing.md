---
title: Processamento de consultas adaptável em bancos de dados Microsoft SQL | Microsoft Docs | Microsoft Docs
description: Recursos de processamento de consulta adaptável para melhorar o desempenho da consulta no SQL Server (2017 e posteriores) e no Banco de Dados SQL do Azure.
ms.custom: ''
ms.date: 07/16/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 979513d43394f4fe5d4e7a2f50166ffae05aded7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39546416"
---
# <a name="adaptive-query-processing-in-sql-databases"></a>Processamento de consultas adaptável em bancos de dados SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Este artigo apresenta estes recursos de processamento de consulta adaptável que você pode usar para melhorar o desempenho da consulta no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]:
- Comentários de concessão de memória do modo de lote.
- Junção adaptável de modo de lote.
- Execução intercalada. 

Em um nível geral, o SQL Server executa uma consulta da seguinte maneira:
1. O processo de otimização de consulta gera um conjunto de planos de execução viáveis para uma consulta específica. Durante esse tempo, o custo das opções de plano é estimado e o plano com o menor custo estimado é usado.
1. O processo de execução de consulta seleciona o plano escolhido pelo otimizador de consulta e o usa para execução.
    
Às vezes, o plano escolhido pelo Otimizador de Consulta não é o ideal por vários motivos. Por exemplo, o número estimado de linhas que passam pelo plano de consulta pode estar incorreto. Os custos estimados ajudam a determinar qual plano é selecionado para ser usado na execução. Se as estimativas de cardinalidade estiverem incorretas, o plano original ainda será usado, apesar das suposições originais erradas.

![Recursos de processamento de consulta adaptável](./media/1_AQPFeatures.png)

### <a name="how-to-enable-adaptive-query-processing"></a>Como habilitar o processamento de consulta adaptável
Você pode deixar as cargas de trabalho automaticamente qualificadas para o processamento de consulta adaptável, habilitando o nível de compatibilidade 140 para o banco de dados.  Você pode definir isso usando o Transact-SQL. Por exemplo:  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 140;
```

## <a name="batch-mode-memory-grant-feedback"></a>Comentários de concessão de memória de modo de lote
Um plano de pós-execução da consulta no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui a memória mínima necessária para execução e o tamanho da concessão de memória ideal para que todas as linhas caibam na memória. Desempenho é prejudicado quando os tamanhos de concessão de memória são dimensionados incorretamente. Concessões excessivas resultam em desperdício de memória e em redução de simultaneidade. Concessões de memória insuficientes causam despejos dispendiosos no disco. Lidando com cargas de trabalho repetitivas, os comentários de concessão de memória de modo de lote recalcula a memória real necessária para uma consulta e atualiza o valor de concessão do plano armazenado em cache.  Quando uma instrução de consulta idêntica for executada, a consulta usará o tamanho de concessão de memória revisado, reduzindo concessões de memória excessivas que afetam a simultaneidade e corrigindo concessões de memória subestimadas que causam despejos dispendiosos no disco.
O gráfico a seguir mostra um exemplo de uso dos comentários de concessão de memória adaptável de modo de lote. Na primeira execução da consulta, a duração foi de **88 segundos** devido à grande quantidade de despejos:   

```sql
DECLARE @EndTime datetime = '2016-09-22 00:00:00.000';
DECLARE @StartTime datetime = '2016-09-15 00:00:00.000';
SELECT TOP 10 hash_unique_bigint_id
FROM dbo.TelemetryDS
WHERE Timestamp BETWEEN @StartTime and @EndTime
GROUP BY hash_unique_bigint_id
ORDER BY MAX(max_elapsed_time_microsec) DESC;
```

![Grande quantidade de despejos](./media/2_AQPGraphHighSpills.png)

Com os comentários de concessão de memória habilitado, na segunda execução, a duração é de **1 segundo** (reduzido dos 88 segundos), os despejos são totalmente removidos e a concessão é maior: 

![Sem despejos](./media/3_AQPGraphNoSpills.png)

### <a name="memory-grant-feedback-sizing"></a>Dimensionamento de comentários de concessão de memória
Para uma condição de concessão de memória excessiva, se a memória concedida for mais de duas vezes o tamanho da memória real usada, os comentários de concessão de memória recalcularão a concessão de memória e atualizarão o plano armazenado em cache. Os planos com concessões de memória abaixo de 1 MB não serão recalculados devido a excedentes.
Para uma condição de concessão de memória de tamanho insuficiente que resulta em um despejo no disco de operadores de modo de lote, os comentários de concessão de memória vão disparar o recálculo da concessão de memória. Os eventos de despejo são relatados para comentários de concessão de memória e podem ser apresentados por meio do XEvent *spilling_report_to_memory_grant_feedback*. Esse evento retorna a ID do nó do plano e o tamanho dos dados despejados desse nó.

### <a name="memory-grant-feedback-and-parameter-sensitive-scenarios"></a>Comentários de concessão de memória e cenários sensíveis a parâmetro
Diferentes valores de parâmetros também podem exigir diferentes planos de consulta para continuarem sendo ideais. Esse tipo de consulta é definido como "sensível a parâmetro". Para planos sensíveis a parâmetro, os comentários de concessão de memória serão desabilitados em uma consulta se ela tiver requisitos de memória instáveis. O plano é desabilitado após várias execuções da consulta repetidas e isso pode ser observado pelo monitoramento do xEvent *memory_grant_feedback_loop_disabled*. Para obter mais informações sobre a detecção de parâmetro e a sensibilidade de parâmetro, veja o [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing).

### <a name="memory-grant-feedback-caching"></a>Armazenamento em cache dos comentários de concessão de memória
Os comentários podem ser armazenados no plano em cache para uma única execução. No entanto, são as execuções consecutivas dessa instrução que se beneficiam dos ajustes dos comentários de concessão de memória. Esse recurso aplica-se à execução repetida de instruções. Os comentários de concessão de memória vão alterar somente o plano armazenado em cache. No momento, as alterações não são capturadas no Repositório de Consultas.
Os comentários não serão mantidos se o plano for removido do cache. Os comentários também serão perdidos se houver um failover. Uma instrução que usa `OPTION (RECOMPILE)` cria um plano e não o armazena em cache. Como ele não é armazenado em cache, nenhum comentário de concessão de memória é produzido e ele não é armazenado para essa compilação e execução.  No entanto, se uma instrução equivalente (ou seja, com o mesmo hash de consulta) que **não** usou `OPTION (RECOMPILE)` for armazenada em cache e, em seguida, executada novamente, a instrução consecutiva poderá se beneficiar dos comentários de concessão de memória.

### <a name="tracking-memory-grant-feedback-activity"></a>Acompanhando a atividade de comentários de concessão de memória
Você pode acompanhar os eventos de comentários de concessão de memória usando o xEvent *memory_grant_updated_by_feedback*. Este evento acompanha o histórico de contagem de execução atual, o número de vezes que o plano foi atualizado por comentários de concessão de memória, a concessão de memória adicional ideal antes da modificação e a concessão de memória adicional ideal depois que os comentários de concessão de memória modificaram o plano armazenado em cache.

### <a name="memory-grant-feedback-resource-governor-and-query-hints"></a>Comentários de concessão de memória, administrador de recursos e dicas de consulta
A memória real concedida cumpre o limite de memória de consulta determinado pela dica de consulta ou pelo administrador de recursos.

### <a name="disabling-memory-grant-feedback-without-changing-the-compatibility-level"></a>Desabilitar comentários de concessão de memória sem alterar o nível de compatibilidade
Comentários de concessão de memória podem ser desabilitados no escopo do banco de dados ou da instrução, mantendo o nível de compatibilidade do banco de dados como 140 e superior. Para desabilitar os comentários de concessão de memória em modo de lotes para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

Quando habilitada, essa configuração aparecerá como habilitada em sys.database_scoped_configurations.

Para reabilitar os comentários de concessão de memória em modo de lotes para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

Você também pode desabilitar os comentários de concessão de memória em modo de lote para uma consulta específica, especificando DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK como uma dica de consulta USE HINT.  Por exemplo:

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK')); 
```

Uma dica de consulta USE HINT tem precedência sobre uma configuração de escopo do banco de dados ou uma configuração de sinalizador de rastreamento.

## <a name="row-mode-memory-grant-feedback"></a>Comentários de concessão de memória do modo de linha
**Aplica-se a**: Banco de Dados SQL como um recurso de visualização pública

Os comentários de concessão de memória de modo de linha expande o recurso de comentários de concessão de memória do modo de lote, ajustando os tamanhos de concessão de memória para operadores de modo de lote e de linha.  

Para habilitar a versão prévia dos comentários de concessão de memória de modo de linha no Banco de Dados SQL, habilite o nível de compatibilidade do banco de dados 150 para o banco de dados ao qual você está conectado ao executar a consulta.

A atividade de comentários de concessão de memória de modo de linha ficará visível por meio do XEvent **memory_grant_updated_by_feedback**. 

Começando com os comentários de concessão de memória de modo de linha, dois novos atributos de plano de consulta serão mostrados para planos pós-execução reais: **IsMemoryGrantFeedbackAdjusted** e **LastRequestedMemory**, que são adicionados ao elemento XML de plano de consulta MemoryGrantInfo. 

LastRequestedMemory mostra a memória concedida em kilobytes (KB) na execução de consulta anterior. O atributo IsMemoryGrantFeedbackAdjusted permite que você verifique o estado dos comentários de concessão de memória para a instrução dentro de um plano de execução de consulta real. Os valores apresentados nesse atributo são os seguintes:

| Valor de IsMemoryGrantFeedbackAdjusted | Descrição |
|--- |--- |
| Não: primeira execução | Os comentários de concessão de memória não ajustam a memória para a primeira compilação e execução associada.  |
| Não: concessão precisa | Se não houver despejo no disco, e a instrução usar pelo menos 50% da memória concedida, os comentários de concessão de memória não serão acionados. |
| Não: comentários desabilitados | Se os comentários de concessão de memória forem acionados continuamente e flutuarem entre as operações de aumento de memória e redução de memória, desabilitaremos os comentários de concessão de memória para a instrução. |
| Sim: ajuste | Os comentários de concessão de memória foram aplicados e podem ser ainda mais ajustados para a próxima execução. |
| Sim: estável | Os comentários de concessão de memória foram aplicados e a memória concedida está estável, ou seja, o que foi concedido para a execução anterior é o mesmo que foi concedido para a execução atual. |

Os atributos de planejamento dos comentários de concessão de memória não são visíveis no momento em planos de execução de consultas gráficas do SQL Server Management Studio. Mas se quiser conferir testes iniciais exiba-os usando o XEvent SET STATISTICS XML ou query_post_execution_showplan.  

## <a name="batch-mode-adaptive-joins"></a>Junções Adaptáveis de modo de lote
O recurso de Junções Adaptáveis de modo de lote permite a escolha de um método de [Junção hash ou de Junção de loops aninhados](../../relational-databases/performance/joins.md) a ser adiado até **depois** que a primeira entrada for verificada. O operador de Junção Adaptável define um limite que é usado para decidir quando mudar para um plano de Loops aninhados. Seu plano, portanto, pode alternar dinamicamente para uma estratégia de junção melhor durante a execução.
Aqui está como isso funciona:
-  Se a contagem de linhas da entrada de junção de build for pequena o suficiente para que uma junção de loops aninhados seja mais ideal do que uma Junção Hash, o plano será alternado para um algoritmo de Loops Aninhados.
-  Se a entrada de junção de build exceder um limite de contagem de linhas específico, o plano não mudará e continuará com uma Junção Hash.

A consulta a seguir é usada para ilustrar um exemplo de Junção Adaptável:

```sql
SELECT  [fo].[Order Key], [si].[Lead Time Days],
[fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 360;
```

A consulta retorna 336 linhas. Habilitando as [Estatísticas de consultas dinâmicas](../../relational-databases/performance/live-query-statistics.MD), podemos ver o plano a seguir:

![Resultados da consulta: 336 linhas](./media/4_AQPStats336Rows.png)

No plano, vemos o seguinte:
1. Temos uma verificação de índice columnstore usado para fornecer linhas para a fase de build da junção hash.
1. Temos o novo operador de Junção Adaptável. Este operador define um limite que é usado para decidir quando mudar para um plano de Loops Aninhados. Para o nosso exemplo, o limite é de 78 linhas. Tudo que for &gt;= 78 linhas usará uma Junção Hash. Quando estiver abaixo do limite, uma junção de Loops Aninhados será usada.
1. Como retornamos 336 linhas, estamos excedendo o limite e, portanto, a segunda branch representa a fase de investigação de uma operação de Junção de Hash padrão. Observe que as Estatísticas de consultas dinâmicas mostram as linhas que passam pelos operadores – nesse caso, "672 de 672".
1. E a última branch é nossa Busca de índice clusterizado a ser usada pela junção de loops aninhados que não teve o limite excedido. Observe que podemos ver "0 de 336" linhas exibidas (a branch não é usada).
 Agora compare o plano com a mesma consulta, mas desta vez para um valor de *Quantidade* que só tem uma linha na tabela:
 
```sql
SELECT  [fo].[Order Key], [si].[Lead Time Days],
[fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 361;
```
A consulta retorna uma linha. Habilitando as Estatísticas de consultas dinâmicas, podemos ver o plano a seguir:

![Resultado da consulta: uma linha](./media/5_AQPStatsOneRow.png)

No plano, vemos o seguinte:
- Com uma linha retornada, a Busca de índice clusterizado agora tem linhas que passam por ela.
- E, como a fase de build da Junção Hash não continuou, não há linhas passando pela segunda branch.

### <a name="adaptive-join-benefits"></a>Benefícios da Junção Adaptável
As cargas de trabalho com oscilações frequentes entre verificações de entradas de junção pequenas e grandes terão mais benefícios com esse recurso.

### <a name="adaptive-join-overhead"></a>Sobrecarga da Junção Adaptável
As junções adaptáveis apresentam um requisito de memória maior do que um plano equivalente de Junção de Loops Aninhados indexados. A memória adicional é solicitada como se os Loops Aninhados fossem uma Junção Hash. Também há sobrecarga para a fase de build como uma operação de “parar e ir” em vez de uma junção equivalente de fluxo de Loops Aninhados. Com esse custo adicional vem a flexibilidade para cenários em que as contagens de linhas podem flutuar na entrada de build.

### <a name="adaptive-join-caching-and-re-use"></a>Armazenamento em cache e reutilização de Junção Adaptável
As Junções Adaptáveis de modo de lote funcionam para a execução inicial de uma instrução e, depois de serem compiladas, as próximas execuções permanecerão adaptáveis com base no limite de Junção Adaptável compilada e nas linhas de tempo de execução que passam pela fase de build da entrada externa.

### <a name="tracking-adaptive-join-activity"></a>Controlando a atividade da Junção Adaptável
O operador de Junção Adaptável tem os seguintes atributos de operador de plano:

| Atributo de plano | Descrição |
|--- |--- |
| AdaptiveThresholdRows | Mostra o uso de limite para alternar de uma junção hash para uma junção de loops aninhados. |
| EstimatedJoinType | Qual é o provável tipo de junção. |
| ActualJoinType | Em um plano real, mostra qual algoritmo de junção foi finalmente escolhido com base no limite. |

O plano estimado mostra a forma do plano de Junção Adaptável, juntamente com um limite de Junção Adaptável definido e o tipo de junção estimado.

### <a name="adaptive-join-and-query-store-interoperability"></a>Interoperabilidade entre junção adaptável e o Repositório de Consultas
O Repositório de Consultas captura e é capaz de forçar um plano de Junção Adaptável de modo de lote.

### <a name="adaptive-join-eligible-statements"></a>Instruções qualificadas para junção adaptável
Algumas condições tornam uma junção lógica qualificada para uma Junção Adaptável de modo de lote:
- O nível de compatibilidade do banco de dados é 140.
- A consulta é uma instrução SELECT (as instruções de modificação de dados não são qualificadas no momento).
- A junção é qualificada para ser executada por uma Junção de Loops Aninhados indexada ou um algoritmo físico de Junção Hash.
- A Junção Hash usa o modo de lote – por meio da presença de um Índice columnstore na consulta geral ou de uma Tabela indexada por columnstore referenciada diretamente pela junção.
- As soluções alternativas geradas da Junção de Loops Aninhados e da Junção Hash devem ter o mesmo primeiro filho (referência externa).

### <a name="adaptive-joins-and-nested-loop-efficiency"></a>Eficiência das junções adaptáveis e de loops aninhados
Se uma Junção Adaptável alterna para uma operação de Loops Aninhados, ela usa as linhas já lidas pelo build de Junção Hash. O operador **não** lê novamente as linhas de referência externa novamente.

### <a name="adaptive-threshold-rows"></a>Linhas de limite adaptável
O gráfico a seguir mostra uma interseção de exemplo entre o custo de uma Junção Hash e o custo de uma alternativa de Junção de Loops Aninhados.  Neste ponto de interseção, o limite é determinado e, por sua vez, ele determina o algoritmo real usado para a operação de junção.

![Limite de junção](./media/6_AQPJoinThreshold.png)

### <a name="disabling-adaptive-joins-without-changing-the-compatibility-level"></a>Desabilitar junções adaptáveis sem alterar o nível de compatibilidade

Junções adaptáveis podem ser desabilitadas no escopo do banco de dados ou da instrução, mantendo o nível de compatibilidade do banco de dados como 140 e superior.  
Para desabilitar as junções adaptáveis para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = ON;
```

Quando habilitada, essa configuração aparecerá como habilitada em sys.database_scoped_configurations.
Para reabilitar as junções adaptáveis para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = OFF;
```

Você também pode desabilitar junções adaptáveis para uma consulta específica, especificando DISABLE_BATCH_MODE_ADAPTIVE_JOINS como uma dica de consulta USE HINT.  Por exemplo:

```sql
SELECT s.CustomerID,
       s.CustomerName,
       sc.CustomerCategoryName
FROM Sales.Customers AS s
LEFT OUTER JOIN Sales.CustomerCategories AS sc
ON s.CustomerCategoryID = sc.CustomerCategoryID
OPTION (USE HINT('DISABLE_BATCH_MODE_ADAPTIVE_JOINS')); 
```

Uma dica de consulta USE HINT tem precedência sobre uma configuração de escopo do banco de dados ou uma configuração de sinalizador de rastreamento.

## <a name="interleaved-execution-for-multi-statement-table-valued-functions"></a>Execução intercalada para funções com valor de tabela de várias instruções
A execução intercalada altera o limite unidirecional entre as fases de execução e de otimização para a execução de uma única consulta e permite que os planos se adaptem com base nas estimativas de cardinalidade revisadas. Durante a otimização, se encontrarmos uma candidata para execução intercalada, que são atualmente **MSTVFs (funções com valor de tabela de várias instruções)**, pausaremos a otimização, executaremos a subárvore aplicável, capturaremos as estimativas de cardinalidade precisas e retomaremos a otimização para operações de downstream.
As MSTVFs têm uma estimativa de cardinalidade fixa de 100 no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e de 1 para versões anteriores. A execução intercalada ajuda com problemas de desempenho da carga de trabalho causado por essas estimativas de cardinalidade fixas associadas às funções com valor de tabela de várias instruções.

A imagem a seguir ilustra uma saída de Estatística de consulta dinâmica, um subconjunto de um plano de execução geral que mostra o impacto de estimativas de cardinalidade fixas de MSTVFs. Você pode ver o fluxo versus de linhas reais versus as linhas estimadas. Há três áreas notáveis do plano (o fluxo é da direita para esquerda):
1. A verificação de tabela de MSTVF tem uma estimativa fixa de 100 linhas. Neste exemplo, no entanto, há 527.597 linhas que passam por essa Verificação de tabela de MSTVF, conforme visto nas Estatísticas de consulta dinâmicas por meio de *527597 de 100* reais das estimadas, portanto a estimativa fixa é significativamente distorcida.
1. Para a operação de loops aninhados, apenas 100 linhas são consideradas retornadas pelo lado externo da junção. Devido ao grande número de linhas que realmente estão sendo retornadas pelo MSTVF, provavelmente melhor usar um algoritmo de junção completamente diferente.
1. Para a operação de correspondência de hash, observe o pequeno símbolo de aviso, que nesse caso está indicando um despejo no disco.

![Fluxo de linha versus estimativa de linhas](./media/7_AQPFlowThreeAreas.png)

Compare o plano anterior com o plano real gerado com a execução intercalada habilitada:

![Plano intercalado](./media/8_AQPInterleavedEnabledPlan.png)

1. Observe que a verificação de tabela de MSTVF agora reflete uma estimativa de cardinalidade precisa. Além disso, observe a reordenação dessa verificação de tabela e das outras operações.
1. E em relação aos algoritmos de junção, mudamos de uma operação de loops aninhados para uma operação de correspondência de hash, que é mais ideal devido ao grande número de linhas envolvidas.
1. Além disso, observe que não há mais avisos de despejo necessários, pois estamos concedendo mais memória, com base na contagem verdadeira de linhas que fluem da verificação da tabela de MSTVF.

### <a name="interleaved-execution-eligible-statements"></a>Instruções qualificadas para execução intercalada
A MSTVF que referencia instruções em execução intercalada deve estar somente leitura e não fazer parte de uma operação de modificação de dados. Além disso, MSTVFs não serão qualificados para execução intercalada se não usarem constantes em tempo de execução.

### <a name="interleaved-execution-benefits"></a>Benefícios de execução intercalada
Em geral, quanto maior a distorção entre o número de linhas real e estimado, juntamente com o número de operações do plano de downstream, maior o impacto no desempenho.
Em geral, a execução intercalada beneficia consultas em que:
1. Há uma grande distorção entre o número de linhas estimado e real para o conjunto de resultados intermediário (neste caso, o MSTVF).
1. E a consulta geral é sensível a uma alteração no tamanho do resultado intermediário. Isso geralmente acontece quando há uma árvore complexa acima dessa subárvore no plano de consulta.
Um simples "SELECT *" de uma MSTVF não se beneficiará da execução intercalada.

### <a name="interleaved-execution-overhead"></a>Sobrecarga da execução intercalada
A sobrecarga deve ser de mínima a nenhuma. As MSTVFs já estavam sendo materializadas antes da introdução da execução intercalada, no entanto a diferença é que, agora estamos permitindo a otimização adiada e, portanto, aproveitando a estimativa de cardinalidade do conjunto de linhas materializadas.
Assim como acontece com qualquer plano que afeta as alterações, alguns planos podem ser alterados de modo que com uma cardinalidade melhor da subárvore podemos obter um plano pior para a consulta geral. A mitigação pode incluir a reversão do nível de compatibilidade ou o uso do Repositório de Consultas para forçar a versão não retornada do plano.

### <a name="interleaved-execution-and-consecutive-executions"></a>Execução intercalada e execuções consecutivas
Depois que um plano de execução intercalada é armazenado em cache, o plano com as estimativas revisadas na primeira execução é usado para as próximas consecutivas sem instanciar novamente a execução intercalada.

### <a name="tracking-interleaved-execution-activity"></a>Controlando a atividade de execução intercalada
Você pode ver os atributos de uso no plano de execução de consulta real:

| Atributo de Plano de execução | Descrição |
| --- | --- |
| ContainsInterleavedExecutionCandidates | Aplica-se ao nó *QueryPlan*. Quando é *true*, significa que o plano contém candidatos a execução intercalada. |
| IsInterleavedExecuted | Atributo do elemento *RuntimeInformation* em RelOp para o nó TVF. Quando *true*, significa que a operação foi materializada como parte de uma operação de execução intercalada. |

Você também pode controlar as ocorrências de execução intercalada por meio dos xEvents a seguir:

| xEvent | Descrição |
| ---- | --- |
| interleaved_exec_status | Esse evento é disparado quando a execução intercalada está ocorrendo. |
| interleaved_exec_stats_update | Esse evento descreve as estimativas de cardinalidade atualizadas por execução intercalada. |
| Interleaved_exec_disabled_reason | Esse evento é disparado quando uma consulta com uma possível candidata para execução intercalada, na verdade, não obtém a execução intercalada. |

Uma consulta deve ser executada para permitir que a execução intercalada revise as estimativas de cardinalidade de MSTVF. No entanto, o plano de execução estimada ainda mostra quando há candidatas para execução intercalada por meio do atributo `ContainsInterleavedExecutionCandidates` do plano de execução.    

### <a name="interleaved-execution-caching"></a>Armazenando em cache de execução intercalada
Se um plano é limpo ou removido do cache, após a execução da consulta há uma nova compilação que usa a execução intercalada.
Uma instrução que usar `OPTION (RECOMPILE)` criará um plano usando a execução intercalada e não a armazenará em cache.     

### <a name="interleaved-execution-and-query-store-interoperability"></a>Interoperabilidade entre execução intercalada e repositório de consultas
Os planos que usam execução intercalada podem ser forçados. O plano é a versão que tem as estimativas de cardinalidade corrigidas com base na execução inicial.    

### <a name="disabling-interleaved-execution-without-changing-the-compatibility-level"></a>Desabilitar execução intercalada sem alterar o nível de compatibilidade

A execução intercalada pode ser desabilitada no escopo do banco de dados ou da instrução, mantendo o nível de compatibilidade do banco de dados como 140 e superior.  Para desabilitar a execução intercalada para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = ON;
```

Quando habilitada, essa configuração aparecerá como habilitada em sys.database_scoped_configurations.
Para reabilitar a execução intercalada para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = OFF;
```

Você também pode desabilitar a execução intercalada para uma consulta específica, especificando DISABLE_INTERLEAVED_EXECUTION_TVF como uma dica de consulta USE HINT.  Por exemplo:

```sql
SELECT  [fo].[Order Key], [fo].[Quantity], [foo].[OutlierEventQuantity]
FROM    [Fact].[Order] AS [fo]
INNER JOIN [Fact].[WhatIfOutlierEventQuantity]('Mild Recession',
                            '1-01-2013',
                            '10-15-2014') AS [foo] ON [fo].[Order Key] = [foo].[Order Key]
                            AND [fo].[City Key] = [foo].[City Key]
                            AND [fo].[Customer Key] = [foo].[Customer Key]
                            AND [fo].[Stock Item Key] = [foo].[Stock Item Key]
                            AND [fo].[Order Date Key] = [foo].[Order Date Key]
                            AND [fo].[Picked Date Key] = [foo].[Picked Date Key]
                            AND [fo].[Salesperson Key] = [foo].[Salesperson Key]
                            AND [fo].[Picker Key] = [foo].[Picker Key]
OPTION (USE HINT('DISABLE_INTERLEAVED_EXECUTION_TVF'));
```

Uma dica de consulta USE HINT tem precedência sobre uma configuração de escopo do banco de dados ou uma configuração de sinalizador de rastreamento.

## <a name="see-also"></a>Consulte Também
[Central de desempenho do Mecanismo de Banco de Dados do SQL Server e do Banco de Dados SQL do Azure](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)    
[Referência de operadores físicos e lógicos de plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Junções](../../relational-databases/performance/joins.md)    
[Demonstrando o Processamento de Consulta Adaptável](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)          

