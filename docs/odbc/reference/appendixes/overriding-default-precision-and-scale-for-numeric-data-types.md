---
title: Substituindo precisão e escala padrão para tipos de dados numéricos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 66fc728440808314dbdaa30065c68232f4a89fba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100608"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Substituir a precisão e a escala padrão para tipos de dados numéricos
Quando o campo SQL_DESC_TYPE em um descartar é definido como SQL_C_NUMERIC, chamando **SQLBindCol** ou **SQLSetDescField**, o campo SQL_DESC_SCALE a descartar estiver definido como 0 e o campo SQL_DESC_PRECISION é definido a precisão de um padrão definido pelo driver. Isso também é verdadeiro quando o campo SQL_DESC_TYPE em um APD é definido para SQL_C_NUMERIC, chamando **SQLBindParameter** ou **SQLSetDescField**. Isso é verdadeiro para entrada, entrada/saída ou parâmetros de saída.  
  
 Se qualquer um dos padrões descritos anteriormente não forem aceitável para um aplicativo, o aplicativo deve definir o campo SQL_DESC_SCALE ou SQL_DESC_PRECISION chamando **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Se o aplicativo chamar **SQLGetData** para retornar dados em uma estrutura de SQL_C_NUMERIC, os campos SQL_DESC_SCALE e SQL_DESC_PRECISION padrão são usados. Se os padrões não forem aceitáveis, o aplicativo deve chamar **SQLSetDescRec** ou **SQLSetDescField** para definir os campos e, em seguida, chame **SQLGetData** com um *TargetType* de SQL_ARD_TYPE para usar os valores nos campos de descritor.  
  
 Quando **SQLPutData** é chamado, a chamada usa os campos SQL_DESC_SCALE e SQL_DESC_PRECISION do registro do descritor que corresponde ao parâmetro de dados em execução ou da coluna, que são campos APD para chamadas para  **SQLExecute** ou **SQLExecDirect**, ou descartar campos para chamadas ao **SQLBulkOperations** ou **SQLSetPos**.
