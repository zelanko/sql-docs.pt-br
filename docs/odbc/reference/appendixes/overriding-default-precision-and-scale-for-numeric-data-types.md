---
title: Substituindo a precisão e escala padrão para tipos de dados numéricos | Microsoft Docs
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
ms.openlocfilehash: 9cfe7bcedb96f5a7ff311d90b5dcdc28fc77b79f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907001"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Substituindo a precisão e escala padrão para tipos de dados numéricos
Quando o campo SQL_DESC_TYPE em um descartar é definido como SQL_C_NUMERIC, chamando **SQLBindCol** ou **SQLSetDescField**, o campo SQL_DESC_SCALE a descartar estiver definido como 0 e o campo SQL_DESC_PRECISION é definido a precisão padrão definidos pelo driver. Isso também é verdadeiro quando o campo SQL_DESC_TYPE em um APD é definido para SQL_C_NUMERIC, chamando **SQLBindParameter** ou **SQLSetDescField**. Isso é verdadeiro para entrada, entrada/saída ou parâmetros de saída.  
  
 Se qualquer um dos padrões descritos anteriormente não são aceitável para um aplicativo, o aplicativo deve definir o campo SQL_DESC_SCALE ou SQL_DESC_PRECISION chamando **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Se o aplicativo chama **SQLGetData** para retornar dados em uma estrutura SQL_C_NUMERIC, os campos SQL_DESC_SCALE e SQL_DESC_PRECISION padrão são usados. Se os padrões não são aceitáveis, o aplicativo deve chamar **SQLSetDescRec** ou **SQLSetDescField** para definir os campos e, em seguida, chamar **SQLGetData** com um *TargetType* de SQL_ARD_TYPE para usar os valores nos campos de descritor.  
  
 Quando **SQLPutData** é chamado, a chamada usa os campos SQL_DESC_SCALE e SQL_DESC_PRECISION de registro do descritor que corresponde ao parâmetro de dados em execução ou coluna, que são os campos APD para chamadas para  **SQLExecute** ou **SQLExecDirect**, ou descartar campos para chamadas para **SQLBulkOperations** ou **SQLSetPos**.
