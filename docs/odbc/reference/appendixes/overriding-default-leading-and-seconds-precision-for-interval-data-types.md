---
title: Substituir à esquerda e a precisão de segundos para tipos de dados de intervalo | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0336aa9334195a706ef59edd7beb1ec482a590d8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>Substituindo à esquerda do padrão e a precisão de segundos para tipos de dados de intervalo
Quando o campo SQL_DESC_TYPE de um descartar é definido como um tipo datetime ou intervalo do C, chamando **SQLBindCol** ou **SQLSetDescField**, o campo SQL_DESC_PRECISION (que contém o intervalo em segundos precisão) é definida para os seguintes padrões:  
  
-   6 de carimbo de hora e todos os tipos de dados de intervalo com um componente de segundos.  
  
-   0 para todos os outros tipos de dados.  
  
 Para todos os tipos de dados de intervalo, o campo do descritor SQL_DESC_DATETIME_INTERVAL_PRECISION, que contém a precisão do campo intervalo à esquerda, é definido como um valor padrão de 2.  
  
 Quando o campo SQL_DESC_TYPE em um APD é definido como um tipo datetime ou intervalo do C, chamando **SQLBindParameter** ou **SQLSetDescField**, o SQL_DESC_PRECISION e SQL_DESC_DATETIME_INTERVAL_ Campos de precisão no APD são definidos como o padrão fornecido anteriormente. Isso é verdadeiro para parâmetros de entrada, mas não para parâmetros de entrada/saída ou de saída.  
  
 Uma chamada para **SQLSetDescRec** define o intervalo de precisão principal para o padrão, mas define a precisão de segundos de intervalo (no campo SQL_DESC_PRECISION) para o valor do seu *precisão* argumento.  
  
 Se qualquer um dos padrões fornecidos anteriormente não é aceitável para um aplicativo, o aplicativo deve definir o campo SQL_DESC_PRECISION ou SQL_DESC_DATETIME_INTERVAL_PRECISION chamando **SQLSetDescField**.  
  
 Se o aplicativo chama **SQLGetData** para retornar dados em um datetime ou intervalo de tipo C, serão usadas a precisão à esquerda do intervalo padrão e a precisão de segundos de intervalo. Se o padrão não for aceitável, o aplicativo deve chamar **SQLSetDescField** para definir o campo de descrição, ou **SQLSetDescRec** definir SQL_DESC_PRECISION. A chamada para **SQLGetData** devem ter um *TargetType* de SQL_ARD_TYPE para usar os valores nos campos de descritor.  
  
 Quando **SQLPutData** é chamado, o intervalo que levam segundos precisão e o intervalo de precisão são lidas dos campos de registro do descritor que correspondem ao parâmetro de dados em execução ou coluna, que são campos APD para chamadas para **SQLExecute** ou **SQLExecDirect**, ou descartar campos para chamadas para **SQLBulkOperations** ou **SQLSetPos**.
