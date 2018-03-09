---
title: "Substituindo a precisão e escala padrão para tipos de dados numéricos | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e2be244dd3ad258ab3fa6b5679e5989d8a08778e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Substituindo a precisão e escala padrão para tipos de dados numéricos
Quando o campo SQL_DESC_TYPE em um descartar é definido como SQL_C_NUMERIC, chamando **SQLBindCol** ou **SQLSetDescField**, o campo SQL_DESC_SCALE a descartar estiver definido como 0 e o campo SQL_DESC_PRECISION é definido a precisão padrão definidos pelo driver. Isso também é verdadeiro quando o campo SQL_DESC_TYPE em um APD é definido para SQL_C_NUMERIC, chamando **SQLBindParameter** ou **SQLSetDescField**. Isso é verdadeiro para entrada, entrada/saída ou parâmetros de saída.  
  
 Se qualquer um dos padrões descritos anteriormente não são aceitável para um aplicativo, o aplicativo deve definir o campo SQL_DESC_SCALE ou SQL_DESC_PRECISION chamando **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Se o aplicativo chama **SQLGetData** para retornar dados em uma estrutura SQL_C_NUMERIC, os campos SQL_DESC_SCALE e SQL_DESC_PRECISION padrão são usados. Se os padrões não são aceitáveis, o aplicativo deve chamar **SQLSetDescRec** ou **SQLSetDescField** para definir os campos e, em seguida, chamar **SQLGetData** com um *TargetType* de SQL_ARD_TYPE para usar os valores nos campos de descritor.  
  
 Quando **SQLPutData** é chamado, a chamada usa os campos SQL_DESC_SCALE e SQL_DESC_PRECISION de registro do descritor que corresponde ao parâmetro de dados em execução ou coluna, que são os campos APD para chamadas para  **SQLExecute** ou **SQLExecDirect**, ou descartar campos para chamadas para **SQLBulkOperations** ou **SQLSetPos**.
