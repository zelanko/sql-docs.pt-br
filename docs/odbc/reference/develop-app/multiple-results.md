---
title: Vários resultados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47e1250a92b78aefdc1611fd88e0ee9b0f772ad0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63254172"
---
# <a name="multiple-results"></a>Vários resultados
Um *resultado* é algo retornado pela fonte de dados depois que uma instrução é executada. ODBC tem dois tipos de resultados: conjuntos de resultados e contagens de linhas. *Contagens de linhas* são o número de linhas afetadas por uma atualização, excluir ou inserir a instrução. Lotes, descrito em [Batches of SQL Statements](../../../odbc/reference/develop-app/batches-of-sql-statements.md), pode gerar vários resultados.  
  
 A seguinte tabela lista os **SQLGetInfo** opções de um aplicativo usa para determinar se uma fonte de dados retorna vários resultados de todos os diferentes tipos de lote. Em particular, uma fonte de dados pode retornar uma contagem de linha única para todo o lote de instruções ou contagens de linhas individuais para cada instrução no lote. No caso de uma resultado gerar o conjunto de instrução executada com uma matriz de parâmetros, a fonte de dados pode retornar um único conjunto de resultados para todos os conjuntos de parâmetros ou conjuntos de resultados individuais para cada conjunto de parâmetros.  
  
|Tipo de lote|Contagens de linhas|Conjuntos de resultados|  
|----------------|----------------|-----------------|  
|Lote explícito|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|Procedimento|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|Matrizes de parâmetros|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] linha gerando a contagem de instruções em um lote podem ter suporte, ainda que o retorno da contagem de linhas não tem suporte. A opção SQL_BATCH_SUPPORT **SQLGetInfo** indica se são permitidas instruções de geração de contagem de linhas em lotes; a opção SQL_BATCH_ROW_COUNTS indica se essas contagens de linhas são retornadas para o aplicativo.  
  
 [b] lotes explícitos e procedimentos sempre retornam vários conjuntos de resultados quando elas incluem várias instruções de geração de conjunto de resultados.  
  
> [!NOTE]  
>  A opção SQL_MULT_RESULT_SETS introduzida no ODBC 1.0 fornece informações apenas gerais sobre se vários conjuntos de resultados podem ser retornados. Em particular, ele é definido como "Y" se os bits SQL_BS_SELECT_EXPLICIT ou SQL_BS_SELECT_PROC são retornados para SQL_BATCH_SUPPORT ou se SQL_PAS_BATCH é retornado para SQL_PARAM_ARRAYS_SELECT.  
  
 Para processar vários resultados, um aplicativo chama **SQLMoreResults**. Essa função descarta o resultado atual e torna o próximo resultado disponível. Ele retorna SQL_NO_DATA quando não houver mais resultados disponíveis. Por exemplo, suponha que as instruções a seguir são executadas como um lote:  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 Depois que essas instruções são executadas, o aplicativo busca linhas do conjunto de resultados criado pelo **selecionar** instrução. Quando isso é feito ao buscar linhas, ele chama **SQLMoreResults** para disponibilizar o número de partes que foram repriced. Se necessário, **SQLMoreResults** descarta linhas não buscadas e fecha o cursor. O aplicativo, em seguida, chama **SQLRowCount** para determinar quantas partes foram repriced pela **atualização** instrução.  
  
 Ele é específica do driver, se a instrução do lote inteiro é executada antes que todos os resultados estejam disponíveis. Em algumas implementações, esse é o caso; em outros, chamando **SQLMoreResults** dispara a execução da próxima instrução no lote.  
  
 Se uma das instruções em um lote falhar, **SQLMoreResults** retornará SQL_ERROR ou SQL_SUCCESS_WITH_INFO. Se o lote foi anulado quando a instrução falhou ou se a instrução com falha foi a última instrução no lote, **SQLMoreResults** retornará SQL_ERROR. Se o lote não foi anulado quando a instrução falhou e a instrução com falha não era a última instrução no lote, **SQLMoreResults** retornará SQL_SUCCESS_WITH_INFO. SQL_SUCCESS_WITH_INFO indica que pelo menos um conjunto de resultados ou contagem foi gerada e que o lote não foi anulado.
