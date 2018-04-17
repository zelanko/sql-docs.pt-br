---
title: Eventos estendidos do monitoramento de instruções de PREVER | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9f56544416d88cc56fed13833667bf689f395693
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="extended-events-for-monitoring-predict-statements"></a>Eventos estendidos para monitoramento de instruções de previsão

Este artigo descreve os eventos estendidos fornecido no SQL Server que você pode usar para monitorar e analisar os trabalhos que usam [PREVER](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) para executar a pontuação em tempo real no SQL Server.

A pontuação em tempo real gera pontuações de uma modelo que foi armazenado no SQL Server de aprendizado de máquina. A função de previsão não exige um tempo de execução externo, como Python, apenas um modelo que foi criado usando um formato binário específico ou de R. Para obter mais informações, consulte [em tempo real de pontuação](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring).

## <a name="prerequisites"></a>Prerequisites

Para obter informações gerais sobre eventos estendidos (às vezes chamados de XEvents) e como controlar os eventos em uma sessão, consulte estes artigos:

+ [Arquitetura e conceitos de eventos estendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [Configurar a captura de evento no SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [Gerenciar sessões de evento no Pesquisador de objetos](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>Tabela de eventos estendidos

Os seguintes eventos estendidos estão disponíveis em todas as versões do SQL Server que oferecem suporte a [T-SQL PREVER](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) instrução, incluindo o SQL Server no Linux e o banco de dados do SQL Azure. 

A instrução T-SQL PREVER foi introduzida no SQL Server 2017. 

|nome |object_type|descrição| 
|----|----|----|
|predict_function_completed |event  |Análise de tempo de execução interna|
|predict_model_cache_hit |event|Ocorre quando um modelo é recuperado do cache de modelo de função de previsão. Use esse evento juntamente com outros eventos predict_model_cache_ * para solucionar problemas ocasionados pelo cache de modelo de função de previsão.|
|predict_model_cache_insert |event  |   Ocorre quando um modelo é inserido em cache de modelo de função de previsão. Use esse evento juntamente com outros eventos predict_model_cache_ * para solucionar problemas ocasionados pelo cache de modelo de função de previsão.    |
|predict_model_cache_miss   |event|Ocorre quando um modelo não foi encontrado no cache de modelo de função de previsão. Ocorrências frequentes deste evento podem indicar que SQL Server precisa de mais memória. Use esse evento juntamente com outros eventos predict_model_cache_ * para solucionar problemas ocasionados pelo cache de modelo de função de previsão.|
|predict_model_cache_remove |event| Ocorre quando um modelo é removido do cache de modelo para a função de previsão. Use esse evento juntamente com outros eventos predict_model_cache_ * para solucionar problemas ocasionados pelo cache de modelo de função de previsão.|

## <a name="query-for-related-events"></a>Consulta de eventos relacionados

Para exibir uma lista de todas as colunas retornadas para esses eventos, execute a seguinte consulta no SQL Server Management Studio:

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>Exemplos

Para obter informações sobre o desempenho de uma sessão de pontuação usando PREVER:

1. Criar um novo estendidos da sessão de evento, usando o Management Studio ou outro suporte [ferramenta](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools).
2. Adicione os eventos `predict_function_completed` e `predict_model_cache_hit` à sessão.
3. Inicie a sessão de evento estendido.
4. Execute a consulta que usa a previsão.

Nos resultados, examine essas colunas:

+ O valor de `predict_function_completed` mostra quanto tempo a consulta gasta no carregamento do modelo e pontuação.
+ O valor booliano `predict_model_cache_hit` indica se a consulta usada um modelo armazenado em cache ou não. 

### <a name="native-scoring-model-cache"></a>Cache de modelo de pontuação nativo

Além dos eventos específicos para previsão, você pode usar as consultas a seguir para obter mais informações sobre o modelo em cache e o uso de cache:

Exiba o cache de modelo de pontuação nativo:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

Exiba os objetos no cache de modelo:

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

