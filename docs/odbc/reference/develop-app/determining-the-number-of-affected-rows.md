---
description: Determinar o número de linhas afetadas
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14114700c4d79f83f0388509056dd0b49bb21a8d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483069"
---
# <a name="determining-the-number-of-affected-rows"></a>Determinar o número de linhas afetadas
Depois que um aplicativo atualiza, exclui ou insere linhas, ele pode chamar **SQLRowCount** para determinar quantas linhas foram afetadas. **SQLRowCount** retorna esse valor se as linhas foram ou não atualizadas, excluídas ou inseridas executando uma instrução **Update**, **delete**ou **Insert** , executando uma instrução UPDATE ou DELETE posicionada ou chamando **SQLSetPos**.  
  
 Se um lote de instruções SQL for executado, a contagem de linhas afetadas poderá ser uma contagem total para todas as instruções no lote ou contagens individuais para cada instrução no lote. Para obter mais informações, consulte [lotes de instruções SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md) e [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 O número de linhas afetadas também é retornado no campo cabeçalho de diagnóstico SQL_DIAG_ROW_COUNT na área de diagnóstico associada ao identificador de instrução. No entanto, os dados nesse campo são redefinidos após cada chamada de função no mesmo identificador de instrução, enquanto o valor retornado por **SQLRowCount** permanece o mesmo até uma chamada para **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**ou **SQLSetPos**.
