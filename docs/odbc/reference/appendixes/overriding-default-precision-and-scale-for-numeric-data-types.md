---
title: Substituindo a precisão e escala padrão para tipos de dados numéricos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 67b017d17566fd19d6d4938bf8ef72d49b7c7bc0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Substituindo a precisão e escala padrão para tipos de dados numéricos
Quando o campo SQL_DESC_TYPE em um descartar é definido como SQL_C_NUMERIC, chamando **SQLBindCol** ou **SQLSetDescField**, o campo SQL_DESC_SCALE a descartar estiver definido como 0 e o campo SQL_DESC_PRECISION é definido a precisão padrão definidos pelo driver. Isso também é verdadeiro quando o campo SQL_DESC_TYPE em um APD é definido para SQL_C_NUMERIC, chamando **SQLBindParameter** ou **SQLSetDescField**. Isso é verdadeiro para entrada, entrada/saída ou parâmetros de saída.  
  
 Se qualquer um dos padrões descritos anteriormente não são aceitável para um aplicativo, o aplicativo deve definir o campo SQL_DESC_SCALE ou SQL_DESC_PRECISION chamando **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Se o aplicativo chama **SQLGetData** para retornar dados em uma estrutura SQL_C_NUMERIC, os campos SQL_DESC_SCALE e SQL_DESC_PRECISION padrão são usados. Se os padrões não são aceitáveis, o aplicativo deve chamar **SQLSetDescRec** ou **SQLSetDescField** para definir os campos e, em seguida, chamar **SQLGetData** com um *TargetType* de SQL_ARD_TYPE para usar os valores nos campos de descritor.  
  
 Quando **SQLPutData** é chamado, a chamada usa os campos SQL_DESC_SCALE e SQL_DESC_PRECISION de registro do descritor que corresponde ao parâmetro de dados em execução ou coluna, que são os campos APD para chamadas para  **SQLExecute** ou **SQLExecDirect**, ou descartar campos para chamadas para **SQLBulkOperations** ou **SQLSetPos**.
