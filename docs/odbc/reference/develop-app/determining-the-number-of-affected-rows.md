---
title: Determinando o número de linhas afetadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a6a1bebf7d5cfb85e49fb0e382dacc4f4464054e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039985"
---
# <a name="determining-the-number-of-affected-rows"></a>Determinar o número de linhas afetadas
Depois que um aplicativo atualiza, exclui ou insere linhas, ele pode chamar **SQLRowCount** para determinar quantas linhas foram afetadas. **SQLRowCount** retorna esse valor se ou não as linhas foram atualizadas, excluídas ou inseridas, executando uma **UPDATE**, **excluir**, ou **inserir** instrução, executando um posicionadas de atualização ou exclusão da instrução ou chamando **SQLSetPos**.  
  
 Se um lote de instruções SQL for executado, a contagem de linhas afetadas pode ser uma contagem total para todas as instruções no lote ou contagens individuais para cada instrução no lote. Para obter mais informações, consulte [Batches of SQL Statements](../../../odbc/reference/develop-app/batches-of-sql-statements.md) e [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 O número de linhas afetadas também é retornado no campo de cabeçalho diagnóstico SQL_DIAG_ROW_COUNT na área de diagnóstico associado com o identificador de instrução. No entanto, os dados nesse campo são redefinidos após a chamada de cada função no mesmo identificador de instrução, enquanto que o valor retornado por **SQLRowCount** permanece o mesmo até que uma chamada para **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**, ou **SQLSetPos**.
