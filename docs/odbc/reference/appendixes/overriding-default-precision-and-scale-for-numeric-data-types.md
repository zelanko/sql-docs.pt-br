---
title: Substituindo a precisão e a escala padrão para tipos de dados numéricos | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100608"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Substituir a precisão e a escala padrão para tipos de dados numéricos
Quando o campo SQL_DESC_TYPE em um ARD é definido como SQL_C_NUMERIC, chamando **SQLBindCol** ou **SQLSetDescField**, o campo SQL_DESC_SCALE no ARD é definido como 0 e o campo SQL_DESC_PRECISION é definido como uma precisão padrão definida pelo driver. Isso também é verdadeiro quando o campo de SQL_DESC_TYPE em um APD é definido como SQL_C_NUMERIC, chamando **SQLBindParameter** ou **SQLSetDescField**. Isso é verdadeiro para parâmetros de entrada, entrada/saída ou saída.  
  
 Se qualquer um dos padrões descritos anteriormente não for aceitável para um aplicativo, o aplicativo deverá definir o SQL_DESC_SCALE ou SQL_DESC_PRECISION campo chamando **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Se o aplicativo chamar **SQLGetData** para retornar dados em uma estrutura de SQL_C_NUMERIC, os campos de SQL_DESC_SCALE e SQL_DESC_PRECISION padrão serão usados. Se os padrões não forem aceitáveis, o aplicativo deverá chamar **SQLSetDescRec** ou **SQLSetDescField** para definir os campos e, em seguida, chamar **SQLGetData** com um *TargetType* de SQL_ARD_TYPE para usar os valores nos campos de descritor.  
  
 Quando **SQLPutData** é chamado, a chamada usa os campos SQL_DESC_SCALE e SQL_DESC_PRECISION do registro de descritor que corresponde à coluna ou ao parâmetro de dados em execução, que são campos APD para chamadas para **SQLExecute** ou **SQLExecDirect**, ou ARD campos para chamadas para **SQLBulkOperations** ou **SQLSetPos**.
