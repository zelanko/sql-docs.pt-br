---
description: Vários resultados
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc42bfa96c4784d232d8359a15ac74b2f3c5a2be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429248"
---
# <a name="multiple-results"></a>Vários resultados
Um *resultado* é algo retornado pela fonte de dados após a execução de uma instrução. O ODBC tem dois tipos de resultados: conjuntos de resultados e contagens de linhas. *Contagens de linhas* são o número de linhas afetadas por uma instrução UPDATE, Delete ou INSERT. Os lotes, descritos em [lotes de instruções SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md), podem gerar vários resultados.  
  
 A tabela a seguir lista as opções de **SQLGetInfo** que um aplicativo usa para determinar se uma fonte de dados retorna vários resultados para cada tipo diferente de lote. Em particular, uma fonte de dados pode retornar uma única contagem de linhas para todo o lote de instruções ou contagens de linhas individuais para cada instrução no lote. No caso de uma instrução de geração de conjunto de resultados executada com uma matriz de parâmetros, a fonte de dados pode retornar um único conjunto de resultados para todos os conjuntos de parâmetros ou conjuntos de resultados individuais para cada conjunto de parâmetros.  
  
|Tipo de lote|Contagens de linhas|Conjuntos de resultados|  
|----------------|----------------|-----------------|  
|Lote explícito|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|Procedimento|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|Matrizes de parâmetros|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] contagem de linhas-as instruções de geração em um lote podem ter suporte, mas o retorno das contagens de linhas não tem suporte. A opção SQL_BATCH_SUPPORT em **SQLGetInfo** indica se as instruções de geração de contagem de linhas são permitidas em lotes; a opção SQL_BATCH_ROW_COUNTS indica se essas contagens de linha são retornadas para o aplicativo.  
  
 [b] lotes e procedimentos explícitos sempre retornam vários conjuntos de resultados quando incluem várias instruções de geração de conjunto de resultados.  
  
> [!NOTE]  
>  A opção SQL_MULT_RESULT_SETS introduzida no ODBC 1,0 fornece apenas informações gerais sobre se vários conjuntos de resultados podem ser retornados. Em particular, ele será definido como "Y" se os bits SQL_BS_SELECT_EXPLICIT ou SQL_BS_SELECT_PROC forem retornados para SQL_BATCH_SUPPORT ou se SQL_PAS_BATCH for retornado para SQL_PARAM_ARRAYS_SELECT.  
  
 Para processar vários resultados, um aplicativo chama **SQLMoreResults**. Essa função descarta o resultado atual e torna o próximo resultado disponível. Ele retorna SQL_NO_DATA quando não há mais resultados disponíveis. Por exemplo, suponha que as instruções a seguir sejam executadas como um lote:  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 Depois que essas instruções são executadas, o aplicativo busca linhas do conjunto de resultados criado pela instrução **Select** . Quando terminar de buscar linhas, ele chama **SQLMoreResults** para disponibilizar o número de partes que foram repreços. Se necessário, **SQLMoreResults** descarta linhas não buscadas e fecha o cursor. Em seguida, o aplicativo chama **SQLRowCount** para determinar quantas partes foram recalculadas pela instrução **Update** .  
  
 Ele é específico de driver se a instrução batch inteira é executada antes de qualquer resultado estar disponível. Em algumas implementações, esse é o caso; em outros, chamar **SQLMoreResults** aciona a execução da próxima instrução no lote.  
  
 Se uma das instruções em um lote falhar, **SQLMoreResults** retornará SQL_ERROR ou SQL_SUCCESS_WITH_INFO. Se o lote tiver sido anulado quando a instrução falhou ou se a instrução com falha fosse a última instrução no lote, **SQLMoreResults** retornará SQL_ERROR. Se o lote não foi anulado quando a instrução falhou e a instrução com falha não foi a última instrução no lote, **SQLMoreResults** retornará SQL_SUCCESS_WITH_INFO. SQL_SUCCESS_WITH_INFO indica que pelo menos um conjunto de resultados ou uma contagem foi gerado e que o lote não foi anulado.
