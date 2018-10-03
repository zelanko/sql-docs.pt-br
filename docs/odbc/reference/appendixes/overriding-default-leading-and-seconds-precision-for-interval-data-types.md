---
title: Substituir líder e a precisão de segundos para tipos de dados Interval | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fdab9e6e60311aca4ce0ae35f92e38c45fdf3702
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687936"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>Substituir precisão inicial e de segundos padrão para tipos de dados de intervalo
Quando o campo SQL_DESC_TYPE de um descartar é definido como um tipo datetime ou intervalo do C, chamando **SQLBindCol** ou **SQLSetDescField**, o campo SQL_DESC_PRECISION (que contém o intervalo em segundos precisão) é definida para os seguintes padrões:  
  
-   6 para o carimbo de data e todos os tipos de dados de intervalo com um componente de segundos.  
  
-   0 para todos os outros tipos de dados.  
  
 Para todos os tipos de dados de intervalo, o campo do descritor SQL_DESC_DATETIME_INTERVAL_PRECISION, que contém a precisão do campo intervalo à esquerda, é definido como um valor padrão de 2.  
  
 Quando o campo SQL_DESC_TYPE em um APD é definido como um tipo datetime ou intervalo do C, chamando **SQLBindParameter** ou **SQLSetDescField**, o SQL_DESC_PRECISION e SQL_DESC_DATETIME_INTERVAL_ Campos de precisão no APD são definidos como o padrão fornecido anteriormente. Isso é verdadeiro para parâmetros de entrada, mas não para os parâmetros de entrada/saída ou de saída.  
  
 Uma chamada para **SQLSetDescRec** define o intervalo de precisão inicial para o padrão, mas define a precisão de segundos de intervalo (no campo SQL_DESC_PRECISION) como o valor de seus *precisão* argumento.  
  
 Se qualquer um dos padrões fornecidos anteriormente não é aceitável para um aplicativo, o aplicativo deve definir o campo SQL_DESC_PRECISION ou SQL_DESC_DATETIME_INTERVAL_PRECISION chamando **SQLSetDescField**.  
  
 Se o aplicativo chamar **SQLGetData** para retornar dados em um datetime ou intervalo de tipo C, serão usadas a precisão à esquerda do intervalo padrão e a precisão de segundos de intervalo. Se o padrão não for aceitável, o aplicativo deve chamar **SQLSetDescField** para definir um campo de descritor, ou **SQLSetDescRec** definir SQL_DESC_PRECISION. A chamada para **SQLGetData** deve ter uma *TargetType* de SQL_ARD_TYPE para usar os valores nos campos de descritor.  
  
 Quando **SQLPutData** é chamado, o intervalo que levam segundos precisão e o intervalo de precisão são lidas dos campos de registro do descritor que correspondem ao parâmetro de dados em execução ou da coluna, que são campos APD para chamadas para **SQLExecute** ou **SQLExecDirect**, ou descartar campos para chamadas para **SQLBulkOperations** ou **SQLSetPos**.
