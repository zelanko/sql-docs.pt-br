---
title: Processamento de consulta inteligente
description: Recursos de processamento inteligente de consulta para melhorar o desempenho da consulta no SQL Server e no Banco de Dados SQL do Azure.
ms.custom: seo-dt-2019
ms.date: 11/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: wiassaf
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83f19187abd2395ef453e59508b2404a7b10a728
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469187"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>Processamento inteligente de consultas em bancos de dados SQL

[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

A família de recursos de IQP (processamento de consulta inteligente) inclui recursos de amplo impacto que melhoram o desempenho de cargas de trabalho existentes com esforço mínimo de implementação na adoção. 

![Processamento de consulta inteligente](./media/iqp-feature-family.png)

Assista a este vídeo de seis minutos para obter uma visão geral do processamento inteligente de consultas:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Intelligent-Query-processing-in-SQL-Server-2019/player?WT.mc_id=dataexposed-c9-niner]


Você pode deixar as cargas de trabalho automaticamente qualificadas para o processamento de consulta inteligente habilitando o nível de compatibilidade do banco de dados aplicável. Você pode definir isso usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por exemplo:  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 150;
```

A tabela a seguir detalha todos os recursos de processamento de consulta inteligente, juntamente com todos os requisitos para o nível de compatibilidade do banco de dados.

| **Recurso IQP** | **Com suporte no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e na [!INCLUDE[ssSDSMIfull](../../includes/sssdsmifull-md.md)]** | **Com suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** |**Descrição** |
| ---------------- | ------- | ------- | ---------------- |
| [Junções adaptáveis (Modo de Lote)](#batch-mode-adaptive-joins) | Sim, no nível de compatibilidade 140| Sim, começando no [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] no nível de compatibilidade 140|As junções adaptáveis selecionam automaticamente um tipo de junção durante o runtime com base nas linhas de entrada reais.|
| [Distinção de contagem aproximada](#approximate-query-processing) | Sim| Sim, no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante|Forneça o COUNT DISTINCT aproximado para cenários de big data com o benefício de alto desempenho e baixo volume de memória. |
| [Modo de Lote no Rowstore](#batch-mode-on-rowstore) | Sim, no nível de compatibilidade 150| Sim, no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante no nível de compatibilidade 150|Forneça o modo de lote para cargas de trabalho de DW relacionais vinculados à CPU sem exigir índices columnstore.  | 
| [Execução intercalada](#interleaved-execution-for-mstvfs) | Sim, no nível de compatibilidade 140| Sim, começando no [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] no nível de compatibilidade 140|Use a cardinalidade real da função com valor de tabela de várias instruções encontrada na primeira compilação em vez de uma estimativa fixa.|
| [Comentários de concessão de memória (Modo de Lote)](#batch-mode-memory-grant-feedback) | Sim, no nível de compatibilidade 140| Sim, começando no [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] no nível de compatibilidade 140|Se uma consulta de modo de lote tiver operações que são despejadas no disco, aumente a memória para execuções consecutivas. Se uma consulta desperdiçar mais de 50% da memória alocada para ela, reduza o lado de concessão de memória para execuções consecutivas.|
| [Comentários de concessão de memória (Modo de Lote)](#row-mode-memory-grant-feedback) | Sim, no nível de compatibilidade 150| Sim, no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante no nível de compatibilidade 150|Se uma consulta de modo de linha tiver operações que são despejadas no disco, aumente a memória para execuções consecutivas. Se uma consulta desperdiçar mais de 50% da memória alocada para ela, reduza o lado de concessão de memória para execuções consecutivas.|
| [Inlining de UDF escalar](#scalar-udf-inlining) | Não | Sim, no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante no nível de compatibilidade 150|Os UDFs escalares são transformados em expressões relacionais equivalentes que são "embutidas" na consulta que fez a chamada, geralmente resultando em ganhos significativos de desempenho.|
| [Compilação Adiada de Variável da Tabela](#table-variable-deferred-compilation) | Sim, no nível de compatibilidade 150| Sim, no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante no nível de compatibilidade 150|Use a cardinalidade real da variável de tabela encontrada na primeira compilação em vez de uma estimativa fixa.|

## <a name="batch-mode-adaptive-joins"></a>Junções adaptáveis de modo de lote
O recurso de Junções Adaptáveis de modo de lote permite que a escolha de um método de [Junção hash ou de Junção de loops aninhados](../../relational-databases/performance/joins.md) seja adiada até **depois** que a primeira entrada for verificada, usando um único plano em cache. O operador de Junção Adaptável define um limite que é usado para decidir quando mudar para um plano de Loops aninhados. Seu plano, portanto, pode alternar dinamicamente para uma estratégia de junção melhor durante a execução.

Para obter mais informações, incluindo como desabilitar junções adaptáveis sem alterar o nível de compatibilidade, confira [Noções básicas sobre junções adaptáveis](../../relational-databases/performance/joins.md#adaptive).

## <a name="batch-mode-memory-grant-feedback"></a>Comentários de concessão de memória de modo de lote
Um plano de pós-execução da consulta no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui a memória mínima necessária para execução e o tamanho da concessão de memória ideal para que todas as linhas caibam na memória. Desempenho é prejudicado quando os tamanhos de concessão de memória são dimensionados incorretamente. Concessões excessivas resultam em desperdício de memória e em redução de simultaneidade. Concessões de memória insuficientes causam despejos dispendiosos no disco. Lidando com cargas de trabalho repetitivas, os comentários de concessão de memória de modo de lote recalcula a memória real necessária para uma consulta e atualiza o valor de concessão do plano armazenado em cache. Quando uma instrução de consulta idêntica for executada, a consulta usará o tamanho de concessão de memória revisado, reduzindo concessões de memória excessivas que afetam a simultaneidade e corrigindo concessões de memória subestimadas que causam despejos dispendiosos no disco.
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
Os comentários não serão mantidos se o plano for removido do cache. Os comentários também serão perdidos se houver um failover. Uma instrução que usa `OPTION (RECOMPILE)` cria um plano e não o armazena em cache. Como ele não é armazenado em cache, nenhum comentário de concessão de memória é produzido e ele não é armazenado para essa compilação e execução. No entanto, se uma instrução equivalente (ou seja, com o mesmo hash de consulta) que **não** usou `OPTION (RECOMPILE)` for armazenada em cache e, em seguida, executada novamente, a instrução consecutiva poderá se beneficiar dos comentários de concessão de memória.

### <a name="tracking-memory-grant-feedback-activity"></a>Acompanhando a atividade de comentários de concessão de memória
Você pode acompanhar os eventos de comentários de concessão de memória usando o xEvent *memory_grant_updated_by_feedback*. Este evento acompanha o histórico de contagem de execução atual, o número de vezes que o plano foi atualizado por comentários de concessão de memória, a concessão de memória adicional ideal antes da modificação e a concessão de memória adicional ideal depois que os comentários de concessão de memória modificaram o plano armazenado em cache.

### <a name="memory-grant-feedback-resource-governor-and-query-hints"></a>Comentários de concessão de memória, administrador de recursos e dicas de consulta
A memória real concedida cumpre o limite de memória de consulta determinado pela dica de consulta ou pelo administrador de recursos.

### <a name="disabling-batch-mode-memory-grant-feedback-without-changing-the-compatibility-level"></a>Desabilitar comentários de concessão de memória de modo de lote sem alterar o nível de compatibilidade
Comentários de concessão de memória podem ser desabilitados no escopo do banco de dados ou da instrução, mantendo o nível de compatibilidade do banco de dados como 140 e superior. Para desabilitar os comentários de concessão de memória em modo de lotes para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = ON;

-- Starting with SQL Server 2019, and in Azure SQL Database
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

Quando habilitada, essa configuração aparecerá como habilitada em [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md).

Para reabilitar os comentários de concessão de memória em modo de lotes para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = OFF;

-- Azure SQL Database, SQL Server 2019 and higher
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

Também é possível desabilitar os comentários de concessão de memória em modo de lote para uma consulta específica designando `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK` como uma [dica de consulta USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint). Por exemplo:

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK')); 
```

Uma dica de consulta USE HINT tem precedência sobre uma configuração de escopo do banco de dados ou uma configuração de sinalizador de rastreamento.

## <a name="row-mode-memory-grant-feedback"></a>Comentários de concessão de memória do modo de linha

**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

Os comentários de concessão de memória de modo de linha expande o recurso de comentários de concessão de memória do modo de lote, ajustando os tamanhos de concessão de memória para operadores de modo de lote e de linha.  

Para habilitar os comentários de concessão de memória em modo de linha no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], habilite o nível de compatibilidade do banco de dados 150 para o banco de dados ao qual você está conectado ao executar a consulta.

A atividade de comentários de concessão de memória de modo de linha ficará visível por meio do XEvent **memory_grant_updated_by_feedback**. 

Começando com os comentários de concessão de memória em modo de linha, dois novos atributos de plano de consulta serão mostrados para planos pós-execução reais: **_IsMemoryGrantFeedbackAdjusted_* _ e _*_LastRequestedMemory_*_, que são adicionados ao elemento XML de plano de consulta _MemoryGrantInfo*. 

*LastRequestedMemory* mostra a memória concedida em quilobytes (KB) na execução de consulta anterior. O atributo *IsMemoryGrantFeedbackAdjusted* permite que você verifique o estado dos comentários de concessão de memória para a instrução dentro de um plano de execução de consulta real. Os valores apresentados nesse atributo são os seguintes:

| Valor de IsMemoryGrantFeedbackAdjusted | Descrição |
|---|---|
| Não: Primeira execução | Os comentários de concessão de memória não ajustam a memória para a primeira compilação e execução associada.  |
| Não: Concessão precisa | Se não houver despejo no disco, e a instrução usar pelo menos 50% da memória concedida, os comentários de concessão de memória não serão acionados. |
| Não: Comentários desabilitados | Se os comentários de concessão de memória forem acionados continuamente e flutuarem entre as operações de aumento de memória e redução de memória, desabilitaremos os comentários de concessão de memória para a instrução. |
| Sim: Ajuste | Os comentários de concessão de memória foram aplicados e podem ser ainda mais ajustados para a próxima execução. |
| Sim: Estável | Os comentários de concessão de memória foram aplicados e a memória concedida está estável, ou seja, o que foi concedido para a execução anterior é o mesmo que foi concedido para a execução atual. |

### <a name="disabling-row-mode-memory-grant-feedback-without-changing-the-compatibility-level"></a>Desabilitar comentários de concessão de memória de modo de linha sem alterar o nível de compatibilidade
Comentários de concessão de memória de modo de linha podem ser desabilitados no escopo do banco de dados ou da instrução, mantendo o nível de compatibilidade do banco de dados como 150 e superior. Para desabilitar os comentários de concessão de memória em modo de linha para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ROW_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

Para reabilitar os comentários de concessão de memória em modo de linha para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ROW_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

Também é possível desabilitar os comentários de concessão de memória em modo de linha para uma consulta específica designando `DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK` como uma [dica de consulta USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint). Por exemplo:

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK')); 
```

Uma dica de consulta USE HINT tem precedência sobre uma configuração de escopo do banco de dados ou uma configuração de sinalizador de rastreamento.

## <a name="interleaved-execution-for-mstvfs"></a>Execução intercalada para MSTVFs
Com a execução intercalada, as contagens de linha reais da função são usadas para tornar decisões de plano de consulta downstream mais embasadas. Confira mais informações sobre MSTVFs (funções com valor de tabela de várias instruções) em [Funções com Valor de Tabela](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF).

A execução intercalada altera o limite unidirecional entre as fases de execução e de otimização para a execução de uma única consulta e permite que os planos se adaptem com base nas estimativas de cardinalidade revisadas. Durante a otimização, se encontrarmos uma candidata para execução intercalada, que são atualmente **MSTVFs (funções com valor de tabela de várias instruções)** , pausaremos a otimização, executaremos a subárvore aplicável, capturaremos as estimativas de cardinalidade precisas e retomaremos a otimização para operações de downstream.   

As MSTVFs têm uma estimativa de cardinalidade fixa de 100 começando com [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e de 1 para versões anteriores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A execução intercalada ajuda com problemas de desempenho da carga de trabalho causado por essas estimativas de cardinalidade fixas associadas às MSTVFs. Para obter mais informações sobre MSTVFs, confira [Criar funções definidas pelo usuário (Mecanismo de Banco de Dados)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF).

A imagem a seguir ilustra uma saída de [Estatísticas de consulta dinâmica](../../relational-databases/performance/live-query-statistics.md), um subconjunto de um plano de execução geral que mostra o impacto de estimativas de cardinalidade fixas de MSTVFs. Você pode ver o fluxo versus de linhas reais versus as linhas estimadas. Há três áreas notáveis do plano (o fluxo é da direita para esquerda):
1. A verificação de tabela de MSTVF tem uma estimativa fixa de 100 linhas. Neste exemplo, no entanto, há 527.597 linhas que passam por essa Verificação de tabela de MSTVF, conforme visto nas Estatísticas de consulta dinâmicas por meio de *527597 de 100* reais das estimadas, portanto a estimativa fixa é significativamente distorcida.
1. Para a operação de loops aninhados, apenas 100 linhas são consideradas retornadas pelo lado externo da junção. Devido ao grande número de linhas que realmente estão sendo retornadas pelo MSTVF, provavelmente melhor usar um algoritmo de junção completamente diferente.
1. Para a operação de correspondência de hash, observe o pequeno símbolo de aviso, que nesse caso está indicando um despejo no disco.

![Fluxo de linha versus estimativa de linhas](./media/7_AQPFlowThreeAreas.png)

Compare o plano anterior com o plano real gerado com a execução intercalada habilitada:

![Plano intercalado](./media/8_AQPInterleavedEnabledPlan.png)

1. Observe que a verificação de tabela de MSTVF agora reflete uma estimativa de cardinalidade precisa. Além disso, observe a reordenação dessa verificação de tabela e das outras operações.
1. E em relação aos algoritmos de junção, mudamos de uma operação de loops aninhados para uma operação de correspondência de hash, que é mais ideal devido ao grande número de linhas envolvidas.
1. Além disso, observe que não há mais avisos de despejo necessários, pois estamos concedendo mais memória com base na contagem verdadeira de linhas que passam da verificação da tabela de MSTVF.

### <a name="interleaved-execution-eligible-statements"></a>Instruções qualificadas para execução intercalada
A MSTVF que referencia instruções em execução intercalada deve estar somente leitura e não fazer parte de uma operação de modificação de dados. Além disso, MSTVFs não serão qualificados para execução intercalada se não usarem constantes em runtime.

### <a name="interleaved-execution-benefits"></a>Benefícios de execução intercalada
Em geral, quanto maior a distorção entre o número de linhas real e estimado, juntamente com o número de operações do plano de downstream, maior o impacto no desempenho.
Em geral, a execução intercalada beneficia consultas em que:
1. Há uma grande distorção entre o número de linhas estimado e real para o conjunto de resultados intermediário (neste caso, o MSTVF).
1. E a consulta geral é sensível a uma alteração no tamanho do resultado intermediário. Isso geralmente acontece quando há uma árvore complexa acima dessa subárvore no plano de consulta.
Um simples `SELECT *` de uma MSTVF não se beneficiará da execução intercalada.

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
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = ON;

-- Starting with SQL Server 2019, and in Azure SQL Database
ALTER DATABASE SCOPED CONFIGURATION SET INTERLEAVED_EXECUTION_TVF = OFF;
```

Quando habilitada, essa configuração aparecerá como habilitada em [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md).
Para reabilitar a execução intercalada para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = OFF;

-- Starting with SQL Server 2019, and in Azure SQL Database
ALTER DATABASE SCOPED CONFIGURATION SET INTERLEAVED_EXECUTION_TVF = ON;
```

Também é possível desabilitar a execução intercalada para uma consulta específica designando `DISABLE_INTERLEAVED_EXECUTION_TVF` como uma [dica de consulta USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint). Por exemplo:

```sql
SELECT [fo].[Order Key], [fo].[Quantity], [foo].[OutlierEventQuantity]
FROM [Fact].[Order] AS [fo]
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

## <a name="table-variable-deferred-compilation"></a>Compilação adiada de variável da tabela

**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

**A compilação adiada de variável da tabela** melhora a qualidade do plano e o desempenho geral para consultas que fazem referência a variáveis de tabela. Durante a otimização e a compilação do plano inicial, esse recurso propagará estimativas de cardinalidade com base nas contagens reais de linha de variável de tabela. Essas informações de contagem de linha precisas serão usadas para otimizar operações de plano de downstream.

Com a compilação adiada de variável de tabela, a compilação de uma instrução que faz referência a uma variável de tabela é adiada até a primeira execução real da instrução. Esse comportamento de compilação adiada é idêntico ao das tabelas temporárias. Essa alteração resulta no uso de cardinalidade real em vez da estimativa original de uma linha. 

Para habilitar a compilação adiada de variável table, habilite o nível de compatibilidade do banco de dados 150 para o banco de dados ao qual você está conectado ao executar a consulta.

A compilação adiada de variável table **não** altera nenhuma outra característica das variáveis de tabela. Por exemplo, esse recurso não adiciona as estatísticas de coluna às variáveis table.

A compilação adiada de variável table **não aumenta a frequência de recompilação**. Em vez disso, ela alterna onde ocorre a compilação inicial. O plano armazenado em cache resultante é gerado com base na contagem da linha de variável table de compilação adiada inicial. O plano armazenado em cache é reutilizado por consultas consecutivas. Ele é reutilizado até que o plano seja removido ou recompilado. 

A contagem de linha de variável de tabela que é usada para a compilação de plano inicial representa um valor típico que pode ser diferente de uma estimativa de contagem de linha fixa. Se ele for diferente, as operações downstream serão beneficiadas. O desempenho poderá não ser melhorado por esse recurso se a contagem de linha da variável table variar consideravelmente entre as execuções.

### <a name="disabling-table-variable-deferred-compilation-without-changing-the-compatibility-level"></a>Desabilitar a compilação adiada de variável de tabela sem alterar o nível de compatibilidade
Desabilitar a compilação adiada de variável table no escopo do banco de dados ou da instrução, mantendo o nível de compatibilidade do banco de dados como 150 e superior. Para desabilitar a compilação adiada de variável table para todas as execuções de consulta originadas do banco de dados, execute o seguinte exemplo dentro do contexto do banco de dados aplicável:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DEFERRED_COMPILATION_TV = OFF;
```

Para habilitar novamente a compilação adiada de variável table para todas as execuções de consulta originadas do banco de dados, execute o seguinte exemplo dentro do contexto do banco de dados aplicável:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DEFERRED_COMPILATION_TV = ON;
```

Você também pode desabilitar a compilação adiada de variável table em uma consulta específica atribuindo DISABLE_DEFERRED_COMPILATION_TV como uma dica de consulta USE HINT.  Por exemplo:

```sql
DECLARE @LINEITEMS TABLE 
    (L_OrderKey INT NOT NULL,
     L_Quantity INT NOT NULL
    );

INSERT @LINEITEMS
SELECT L_OrderKey, L_Quantity
FROM dbo.lineitem
WHERE L_Quantity = 5;

SELECT O_OrderKey,
    O_CustKey,
    O_OrderStatus,
    L_QUANTITY
FROM    
    ORDERS,
    @LINEITEMS
WHERE    O_ORDERKEY    =    L_ORDERKEY
    AND O_OrderStatus = 'O'
OPTION (USE HINT('DISABLE_DEFERRED_COMPILATION_TV'));
```

## <a name="scalar-udf-inlining"></a>Embutimento de UDF escalar

**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)])

O inlining da UDF escalar transforma automaticamente [UDFs escalares](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar) em expressões relacionais. Ele as incorpora à chamada da consulta SQL. Essa transformação melhora o desempenho de cargas de trabalho que aproveitam as UDFs escalares. O inlining da UDF escalar facilita a otimização baseada em custo de operações das UDFs. Os resultados são eficientes, orientados para conjunto e paralelos, em vez de planos de execução ineficientes, iterativos e seriais. Esse recurso é habilitado por padrão no nível de compatibilidade do banco de dados 150.

Para saber mais, confira [Scalar UDF Inlining](../user-defined-functions/scalar-udf-inlining.md) (Embutimento de UDF escalar).

## <a name="approximate-query-processing"></a>Processamento de consulta aproximada

**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

O processamento de consulta aproximado é uma nova família de recursos. Ele agrega grandes conjuntos de dados nos quais a capacidade de resposta é mais importante do que a precisão absoluta. Um exemplo é o cálculo de **COUNT(DISTINCT())** entre 10 bilhões de linhas para a exibição em um painel. Nesse caso, o que é importante não é a precisão absoluta, mas a capacidade de resposta que é essencial. A nova função de agregação **APPROX_COUNT_DISTINCT** retorna o número aproximado de valores não nulos exclusivos em um grupo.

Para saber mais, confira [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md).

## <a name="batch-mode-on-rowstore"></a>Modo de Lote no Rowstore 

**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

O modo de lote em rowstore permite que a execução em modo de lote para cargas de trabalho analíticas sem a necessidade de índices columnstore.  Esse recurso dá suporte a filtros de bitmap e à execução do modo de lote para em disco heaps e índices de árvore B. O modo de lote em rowstore habilita o suporte para todos os operadores habilitados para o modo de lote existente.

### <a name="background"></a>Segundo plano
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] introduziu um novo recurso para acelerar as cargas de trabalho analíticas: os índices columnstore. Expandimos os casos de uso e melhoramos o desempenho de índices columnstore em todas as versões subsequentes. Até agora, apresentamos e documentamos todos esses recursos como um único recurso. Você pode criar índices columnstore em suas tabelas. E sua carga de trabalho analítica será bem mais rápida. No entanto, há dois conjuntos de tecnologias relacionados mas distintos:
- Com os índices **columnstore**, as consultas analíticas acessam apenas os dados que elas precisam das colunas. A compactação de página no formato columnstore também é mais eficiente do que a dos índices **rowstore** tradicionais. 
- Com o processamento em **modo de lote**, os operadores de consulta processam dados com mais eficiência. Eles funcionam em um lote de linhas em vez de uma linha por vez. Diversos outros aprimoramentos de escalabilidade estão ligados ao processamento do modo de lote. Confira mais informações sobre o modo de lote em [Modos de execução](../../relational-databases/query-processing-architecture-guide.md#execution-modes).

Os dois conjuntos de recursos funcionam juntos para melhorar o uso de CPU e E/S (entrada/saída):
- ao usar índices columnstore, mais dos seus dados se encaixam na memória. Isso reduz a carga de trabalho de E/S.
- O processamento de modo de lote usa a CPU com mais eficiência.

As duas tecnologias tiram proveito um do outro sempre que possível. Por exemplo, agregações de modo de lote podem ser avaliadas como parte de uma verificação de índice columnstore. Os dados de columnstore compactados também são processados usando a codificação de tamanho de execução com muito mais eficiência com junções e agregações de modos de lotes. 
 
No entanto, é importante entender que os dois recursos são independentes:
* Você pode obter planos de modo de linha que usam índices columnstore.
* Você pode obter planos de modo de linha que usam somente índices rowstore. 

Geralmente é possível obter os melhores resultados ao usar os dois recursos juntos. Portanto, até agora, o otimizador de consulta do SQL Server considerou o processamento de modo de lote só para consultas que envolvem pelo menos uma tabela com um índice columnstore.

Os índices columnstore podem não ser apropriados para alguns aplicativos. Pode ser que o aplicativo use outro recurso que não tenha suporte com índices columnstore. Por exemplo, as modificações no local não são compatíveis com a compactação de columnstore. Assim, os gatilhos não têm suporte em tabelas com índices columnstore clusterizados. E, mais importante, índices columnstore adicionam uma sobrecarga para as instruções **DELETE** e **UPDATE**. 

Para algumas cargas de trabalho transacionais analíticas híbridas, a sobrecarga de uma carga de trabalho transacional supera os benefícios obtidos do uso de índices columnstore. Esses cenários podem se beneficiar do uso aprimorado da CPU empregando o processamento do modo de lote sozinho. É por isso que o recurso batch-mode-on-rowstore considera o modo de lote para todas as consultas independentemente de qual tipo de índice está envolvido.

### <a name="workloads-that-might-benefit-from-batch-mode-on-rowstore"></a>Cargas de trabalho que podem se beneficiar com o modo de lote no rowstore
As seguintes cargas de trabalho podem se beneficiar do modo de lote no rowstore:
* Uma parte significativa da carga de trabalho consiste em consultas analíticas. Em geral, essas consultas usam operadores como junções ou agregações que processam centenas de milhares de linhas ou mais.
* A carga de trabalho está associada à CPU. Se o gargalo for em E/S, ainda será recomendável que você considere um índice columnstore, se possível.
* Criar um índice columnstore adiciona muita sobrecarga à parte transacional da carga de trabalho. Ou a criação de um índice columnstore não é viável porque seu aplicativo depende de um recurso que ainda não tem suporte com índices columnstore.


> [!NOTE]
> O modo de lote em rowstore só pode ajudar a reduzir o consumo de CPU. Se o gargalo for relacionado à E/S e os dados ainda não estiverem armazenados em cache (cache "frio"), o modo de lote em rowstore não vai melhorar o tempo decorrido da consulta. Da mesma forma, se não houver memória o bastante no computador para armazenar em cache todos os dados, será improvável que ocorra uma melhoria de desempenho.

### <a name="what-changes-with-batch-mode-on-rowstore"></a>O que muda com o modo de lote no rowstore?

Defina o banco de dados para o nível de compatibilidade 150. Nenhuma outra alteração é necessária.

Mesmo que uma consulta não acesse nenhuma tabela com índices columnstore, o processador de consultas, usando heurística, decidirá se deve considerar o modo de lote. A heurística consiste destas verificações:
1. Uma verificação inicial dos tamanhos de tabela, operadores usados e cardinalidades estimadas na consulta de entrada.
2. Pontos de verificação adicionais à medida que o otimizador descobre planos novos e mais baratos para a consulta. Se esses planos alternativos não usarem o modo de lote de forma significativa, o otimizador parará de explorar as alternativas de modo de lote.

Se o modo de lote em rowstore for usado, você verá o modo de execução real como o **modo de lote** no plano de consulta. O operador de verificação usa o modo de lote em heaps em discos e índices de árvore B. Essa verificação do modo de lote pode avaliar os filtros de bitmap do modo de lote. Você também poderá ver outros operadores de modo de lote no plano. Os exemplos são junções hash, agregações baseadas em hash, classificações, agregações de janela, filtros, concatenações e operadores escalares de computação.

### <a name="remarks"></a>Comentários

Planos de consulta nem sempre usam o modo de lote. O otimizador de consulta pode decidir que o modo de lote não é útil para a consulta. 

O espaço de pesquisa do otimizador de consulta está sendo alterado. Portanto, se você receber um plano de modo de linha, poderia não ser o mesmo que o plano que você obtém em um nível de compatibilidade mais baixo. E se você receber um plano de modo de lote, poderia não ser o mesmo que o plano que você obtém com um índice columnstore. 

Os planos também podem alterar as consultas que combinam os índices columnstore e rowstore devido à verificação de rowstore do novo modo de lote.

Existem limitações atuais para o novo modo de lote na verificação de rowstore: 
- Ele não será iniciado para tabelas OLTP na memória nem para índices diferentes de heaps em disco e árvores B. 
- Ele também não será iniciado ao buscar ou filtrar uma coluna LOB (de objeto grande). Essa limitação inclui conjuntos de colunas esparsas e colunas XML.

Há consultas em que o modo de lote não é usado para pares em índices columnstore. Os exemplos são consultas que envolvem cursores. Essas mesmas exclusões também se estendem ao modo de lote em rowstore.

### <a name="configure-batch-mode-on-rowstore"></a>Configurar o modo de lote no rowstore
A configuração no escopo do banco de dados **BATCH_MODE_ON_ROWSTORE** é ativada por padrão. Ela desabilita o modo de lote em rowstore sem exigir uma alteração no nível de compatibilidade do banco de dados:

```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```

você pode desabilitar o modo de lote em rowstore por meio de configuração do escopo do banco de dados. Mas você ainda pode substituir a configuração no nível da consulta usando a dica de consulta **ALLOW_BATCH_MODE**. O exemplo a seguir habilita o modo de lote no rowstore, mesmo com o recurso desabilitado por meio de configuração com escopo do banco de dados:

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```

Também é possível desabilitar o modo de lote em rowstore para uma consulta específica usando a dica de consulta **DISALLOW_BATCH_MODE**. Consulte o seguinte exemplo:

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('DISALLOW_BATCH_MODE'));
```

## <a name="see-also"></a>Confira também
[Central de desempenho do Mecanismo de Banco de Dados do SQL Server e do Banco de Dados SQL do Azure](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)    
[Referência de operadores físicos e lógicos do plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Junções](../../relational-databases/performance/joins.md)       
[Demonstrar o processamento de consulta inteligente](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/intelligent-query-processing)   
