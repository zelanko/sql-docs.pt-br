---
title: Eventos estendidos para monitoramento de instruções PREDICT - serviços do SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e680da7485069e6838edff260a505461a22c472b
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432239"
---
# <a name="extended-events-for-monitoring-predict-statements"></a>Eventos estendidos para monitoramento de instruções PREDICT

Este artigo descreve os eventos estendidos, fornecido no SQL Server que você pode usar para monitorar e analisar os trabalhos que usam [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) executar pontuação em tempo real no SQL Server.

Pontuação em tempo real gera as pontuações de um modelo de machine learning que foram armazenado no SQL Server. A função PREDICT não exige um tempo de execução externo, como R ou Python, apenas um modelo que foi criado usando um formato binário específico. Para obter mais informações, consulte [em tempo real de pontuação](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring).

## <a name="prerequisites"></a>Prerequisites

Para obter informações gerais sobre eventos estendidos (às vezes chamados de XEvents) e como controlar os eventos em uma sessão, consulte estes artigos:

+ [Arquitetura e conceitos de eventos estendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [Configurar a captura de evento no SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [Gerenciar sessões de evento no Pesquisador de objetos](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>Tabela de eventos estendidos

Os seguintes eventos estendidos estão disponíveis em todas as versões do SQL Server que dão suporte a [PREVER o T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) instrução, incluindo o SQL Server no Linux e no banco de dados SQL. 

A instrução T-SQL PREVER foi introduzida no SQL Server 2017. 

|nome |object_type|descrição| 
|----|----|----|
|predict_function_completed |event  |Divisão de tempo de execução interno|
|predict_model_cache_hit |event|Ocorre quando um modelo é recuperado do cache de modelo da função PREDICT. Use esse evento junto com outros eventos predict_model_cache _ * para solucionar problemas causados pelo cache de modelo da função PREDICT.|
|predict_model_cache_insert |event  |   Ocorre quando um modelo é inserido no cache de modelo da função PREDICT. Use esse evento junto com outros eventos predict_model_cache _ * para solucionar problemas causados pelo cache de modelo da função PREDICT.    |
|predict_model_cache_miss   |event|Ocorre quando um modelo não for encontrado no cache de modelo da função PREDICT. Ocorrências frequentes deste evento podem indicar que SQL Server precisa de mais memória. Use esse evento junto com outros eventos predict_model_cache _ * para solucionar problemas causados pelo cache de modelo da função PREDICT.|
|predict_model_cache_remove |event| Ocorre quando um modelo é removido do cache de modelo para a função PREDICT. Use esse evento junto com outros eventos predict_model_cache _ * para solucionar problemas causados pelo cache de modelo da função PREDICT.|

## <a name="query-for-related-events"></a>Consulta de eventos relacionados

Para exibir uma lista de todas as colunas retornadas para esses eventos, execute a seguinte consulta no SQL Server Management Studio:

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>Exemplos

Para capturar informações sobre o desempenho de uma sessão de pontuação usando PREVER:

1. Criar um novo estendidos da sessão de evento, usando o Management Studio ou outro com suporte [ferramenta](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools).
2. Adicione os eventos `predict_function_completed` e `predict_model_cache_hit` à sessão.
3. Inicie a sessão de evento estendido.
4. Execute a consulta que usa PREDICT.

Nos resultados, examine estas colunas:

+ O valor para `predict_function_completed` mostra quanto tempo a consulta gasta em carregar o modelo e pontuação.
+ O valor booliano para `predict_model_cache_hit` indica se a consulta usada um modelo armazenado em cache ou não. 

### <a name="native-scoring-model-cache"></a>Cache de modelo de pontuação nativa

Além dos eventos específicos a PREVER, você pode usar as consultas a seguir para obter mais informações sobre o modelo armazenado em cache e o uso de cache:

Exiba o cache de modelo de pontuação nativa:

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

