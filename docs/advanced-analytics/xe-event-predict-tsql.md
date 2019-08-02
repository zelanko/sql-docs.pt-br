---
title: Eventos estendidos para monitoramento de instruções PREDICT
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 283e128285fc50b9109d7950b171e30224fb9692
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714638"
---
# <a name="extended-events-for-monitoring-predict-statements"></a>Eventos estendidos para monitoramento de instruções PREDICT

Este artigo descreve os eventos estendidos fornecidos no SQL Server que você pode usar para monitorar e analisar trabalhos que usam a [previsão](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) para executar a pontuação em tempo real em SQL Server.

A pontuação em tempo real gera pontuações de um modelo de aprendizado de máquina que foi armazenado no SQL Server. A função PREDICT não requer um tempo de execução externo, como R ou Python, apenas um modelo que tenha sido criado usando um formato binário específico. Para obter mais informações, consulte [Pontuação em tempo real](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring).

## <a name="prerequisites"></a>Pré-requisitos

Para obter informações gerais sobre eventos estendidos (às vezes chamados de XEvents) e como rastrear eventos em uma sessão, consulte estes artigos:

+ [Arquitetura e conceitos de eventos estendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [Configurar a captura de eventos no SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [Gerenciar sessões de evento no Pesquisador de objetos](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>Tabela de eventos estendidos

Os eventos estendidos a seguir estão disponíveis em todas as versões do SQL Server que dão suporte à instrução de [previsão T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) , incluindo SQL Server em Linux e banco de dados SQL do Azure. 

A instrução T-SQL PREDICT foi introduzida no SQL Server 2017. 

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
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
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

