---
title: Monitorar o T-SQL de previsão com eventos estendidos
description: Saiba como usar eventos estendidos para monitorar e solucionar problemas de instruções T-SQL de previsão no Serviços de Machine Learning SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 958ac3e24a9deec231e7fd4d5da14477d693f4de
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714300"
---
# <a name="monitor-predict-t-sql-statements-with-extended-events-in-sql-server-machine-learning-services"></a>Monitorar instruções T-SQL de previsão com eventos estendidos no SQL Server Serviços de Machine Learning

Saiba como usar eventos estendidos para monitorar e solucionar problemas de instruções T-SQL de [previsão](../../t-sql/queries/predict-transact-sql.md) no serviços de Machine Learning SQL Server.

## <a name="table-of-extended-events"></a>Tabela de eventos estendidos

Os eventos estendidos a seguir estão disponíveis em todas as versões do SQL Server que dão suporte à instrução T-SQL de [previsão](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) . 

|name |object_type|description| 
|----|----|----|
|predict_function_completed |event  |Divisão do tempo de execução Builtin|
|predict_model_cache_hit |event|Ocorre quando um modelo é recuperado do cache de modelo de função de previsão. Use esse evento junto com outros eventos predict_model_cache_ * para solucionar problemas causados pelo cache de modelo de função de previsão.|
|predict_model_cache_insert |event  |   Ocorre quando um modelo é inserido no cache de modelo de função de previsão. Use esse evento junto com outros eventos predict_model_cache_ * para solucionar problemas causados pelo cache de modelo de função de previsão.    |
|predict_model_cache_miss   |event|Ocorre quando um modelo não é encontrado no cache de modelo de função de previsão. Ocorrências frequentes desse evento podem indicar que SQL Server precisa de mais memória. Use esse evento junto com outros eventos predict_model_cache_ * para solucionar problemas causados pelo cache de modelo de função de previsão.|
|predict_model_cache_remove |event| Ocorre quando um modelo é removido do cache de modelo para a função de previsão. Use esse evento junto com outros eventos predict_model_cache_ * para solucionar problemas causados pelo cache de modelo de função de previsão.|

## <a name="query-for-related-events"></a>Consultar eventos relacionados

Para exibir uma lista de todas as colunas retornadas para esses eventos, execute a seguinte consulta no SQL Server Management Studio:

```sql
SELECT * 
FROM sys.dm_xe_object_columns 
WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>Exemplos

Para capturar informações sobre o desempenho de uma sessão de Pontuação usando PREDICT:

1. Crie uma nova sessão de evento estendido, usando Management Studio ou outra [ferramenta](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)com suporte.
2. Adicione os eventos `predict_function_completed` e `predict_model_cache_hit` à sessão.
3. Inicie a sessão de evento estendido.
4. Execute a consulta que usa PREDICT.

Nos resultados, examine estas colunas:

+ O valor de `predict_function_completed` mostra quanto tempo a consulta gastou ao carregar o modelo e a pontuação.
+ O valor booliano `predict_model_cache_hit` para indica se a consulta usou um modelo em cache ou não. 

### <a name="native-scoring-model-cache"></a>Cache de modelo de Pontuação nativa

Além dos eventos específicos da previsão, você pode usar as consultas a seguir para obter mais informações sobre o uso do cache e do modelo em cache:

Exibir o cache de modelo de Pontuação nativa:

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

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre eventos estendidos (às vezes chamados de XEvents) e como rastrear eventos em uma sessão, consulte estes artigos:

+ [Monitorar scripts do Python e do R com eventos estendidos no SQL Server Serviços de Machine Learning](extended-events.md)
+ [Arquitetura e conceitos de eventos estendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [Configurar a captura de eventos no SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [Gerenciar sessões de evento no Pesquisador de objetos](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)
