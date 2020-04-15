---
title: Múltiplos Resultados | Microsoft Docs
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
ms.openlocfilehash: d90414b631a7e81a7868ab7974b64ea84a0ea452
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302404"
---
# <a name="multiple-results"></a>Vários resultados
Um *resultado* é algo devolvido pela fonte de dados após a execução de uma declaração. A ODBC tem dois tipos de resultados: conjuntos de resultados e contagem de linhas. *Contagem de linhas* é o número de linhas afetadas por uma instrução de atualização, exclusão ou inserção. Os lotes, [descritos em lotes de instruções SQL,](../../../odbc/reference/develop-app/batches-of-sql-statements.md)podem gerar vários resultados.  
  
 A tabela a seguir lista as opções **SQLGetInfo** que um aplicativo usa para determinar se uma fonte de dados retorna vários resultados para cada tipo diferente de lote. Em particular, uma fonte de dados pode retornar uma única contagem de linhas para todo o lote de declarações ou contagens individuais de linha para cada declaração no lote. No caso de uma declaração de geração de conjunto de resultados executada com um conjunto de parâmetros, a fonte de dados pode retornar um único conjunto de resultados para todos os conjuntos de parâmetros ou conjuntos de resultados individuais para cada conjunto de parâmetros.  
  
|Tipo de lote|Contagem de linhas|Conjuntos de resultados|  
|----------------|----------------|-----------------|  
|Lote explícito|SQL_BATCH_ROW_COUNT[a]|-[b]|  
|Procedimento|SQL_BATCH_ROW_COUNT[a]|-[b]|  
|Matrizes de parâmetros|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] As instruções de geração de contagem de linhas em um lote podem ser suportadas, mas o retorno das contagens de linha não suportadas. A opção SQL_BATCH_SUPPORT no **SQLGetInfo** indica se as instruções de geração de contagem de linhas são permitidas em lotes; a opção SQL_BATCH_ROW_COUNTS indica se essas contagens de linha são devolvidas ao aplicativo.  
  
 [b] Lotes e procedimentos explícitos sempre retornam vários conjuntos de resultados quando incluem várias instruções de geração de resultados.  
  
> [!NOTE]  
>  A opção SQL_MULT_RESULT_SETS introduzida no ODBC 1.0 fornece apenas informações gerais sobre se vários conjuntos de resultados podem ser retornados. Em particular, é definido como "Y" se os bits SQL_BS_SELECT_EXPLICIT ou SQL_BS_SELECT_PROC forem devolvidos para SQL_BATCH_SUPPORT ou se SQL_PAS_BATCH for devolvido para SQL_PARAM_ARRAYS_SELECT.  
  
 Para processar vários resultados, um aplicativo chama **SQLMoreResults**. Esta função descarta o resultado atual e disponibiliza o próximo resultado. Ele retorna SQL_NO_DATA quando não há mais resultados disponíveis. Por exemplo, suponha que as seguintes instruções sejam executadas como um lote:  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 Depois que essas instruções são executadas, o aplicativo busca linhas do conjunto de resultados criado pela instrução **SELECT.** Quando é feito buscar linhas, ele chama **SQLMoreResults** para disponibilizar o número de peças que foram reprecificadas. Se necessário, **o SQLMoreResults** descarta linhas não necessárias e fecha o cursor. Em seguida, o aplicativo chama **o SQLRowCount** para determinar quantas peças foram reprecificadas pela declaração **UPDATE.**  
  
 É específico do driver se toda a instrução de lote é executada antes de qualquer resultado estar disponível. Em algumas implementações, este é o caso; em outros, chamar **SQLMoreResults** desencadeia a execução da próxima declaração no lote.  
  
 Se uma das instruções em um lote falhar, **o SQLMoreResults** retornará SQL_ERROR ou SQL_SUCCESS_WITH_INFO. Se o lote foi abortado quando a declaração falhou ou a declaração falha foi a última declaração no lote, o **SQLMoreResults** retornará SQL_ERROR. Se o lote não foi abortado quando a declaração falhou e a declaração falha não foi a última declaração no lote, o **SQLMoreResults** retornará SQL_SUCCESS_WITH_INFO. SQL_SUCCESS_WITH_INFO indica que pelo menos um conjunto de resultados ou contagem foi gerado e que o lote não foi abortado.
