---
title: Determinar o número de linhas afetadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3736f620e311f51ebd97ee99e71830722c2ee367
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="determining-the-number-of-affected-rows"></a>Determinar o número de linhas afetadas
Depois que um aplicativo atualiza, exclui ou insere linhas, ele pode chamar **SQLRowCount** para determinar quantas linhas foram afetadas. **SQLRowCount** retorna esse valor se ou não as linhas foram atualizadas, excluídas ou inseridas executando um **atualização**, **excluir**, ou **inserir** instrução, executando um posicionadas de atualização ou exclusão da instrução ou chamando **SQLSetPos**.  
  
 Se um lote de instruções SQL for executado, a contagem de linhas afetadas pode ser uma contagem total para todas as instruções no lote ou contas individuais para cada instrução no lote. Para obter mais informações, consulte [Batches of SQL Statements](../../../odbc/reference/develop-app/batches-of-sql-statements.md) e [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 O número de linhas afetadas também é retornado no campo de cabeçalho de diagnóstico SQL_DIAG_ROW_COUNT na área de diagnóstico associado com o identificador de instrução. No entanto, os dados nesse campo são redefinidos após cada função de chamada no identificador da instrução, enquanto o valor retornado por **SQLRowCount** permanecerá o mesmo até que uma chamada para **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**, ou **SQLSetPos**.
