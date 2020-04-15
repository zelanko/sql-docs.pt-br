---
title: Sobrepondo a precisão e a escala padrão para tipos de dados numéricos | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365c5f69d21dd3a4ad8e89805d81f1b3b0c9dcba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303587"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Substituir a precisão e a escala padrão para tipos de dados numéricos
Quando o campo de SQL_DESC_TYPE em um ARD é definido como SQL_C_NUMERIC, chamando **sqlBindCol** ou **SQLSetDescField**, o campo de SQL_DESC_SCALE no ARD é definido como 0 e o campo SQL_DESC_PRECISION é definido como uma precisão padrão definida pelo driver. Isso também é verdade quando o campo de SQL_DESC_TYPE em um APD é definido como SQL_C_NUMERIC, chamando **sQLBindParameter** ou **SQLSetDescField**. Isso é verdadeiro para parâmetros de entrada, entrada/saída ou de saída.  
  
 Se qualquer um dos padrões descritos anteriormente não for aceitável para um aplicativo, o aplicativo deverá definir o campo SQL_DESC_SCALE ou SQL_DESC_PRECISION ligando para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Se o aplicativo chamar **o SQLGetData** para retornar dados em uma estrutura SQL_C_NUMERIC, os campos padrão SQL_DESC_SCALE e SQL_DESC_PRECISION serão usados. Se os padrões não forem aceitáveis, o aplicativo deve chamar **SQLSetDescRec** ou **SQLSetDescField** para definir os campos e, em seguida, chamar **SQLGetData** com um *TargetType* de SQL_ARD_TYPE para usar os valores nos campos descritores.  
  
 Quando **o SQLPutData** é chamado, a chamada usa os campos SQL_DESC_SCALE e SQL_DESC_PRECISION do registro descritor que corresponde ao parâmetro ou coluna data-at-execution, que são campos APD para chamadas para **sQLExecute** ou **SQLExecDirect,** ou campos ARD para chamadas para **SQLBulkOperations** ou **SQLSetPos**.
