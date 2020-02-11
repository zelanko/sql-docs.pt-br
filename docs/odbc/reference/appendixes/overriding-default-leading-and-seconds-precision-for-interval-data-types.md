---
title: Substituir a precisão inicial e de segundos para tipos de dados de intervalo | Microsoft Docs
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
ms.openlocfilehash: 13adfb16b772acc5fac30cf3d10c6199f16f479d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100620"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>Substituir precisão inicial e de segundos padrão para tipos de dados de intervalo
Quando o campo de SQL_DESC_TYPE de um ARD é definido como um tipo de data/hora ou intervalo C, chamando **SQLBindCol** ou **SQLSetDescField**, o campo SQL_DESC_PRECISION (que contém a precisão de segundos de intervalo) é definido com os seguintes padrões:  
  
-   6 para carimbo de data/hora e todos os tipos de dados de intervalo com um segundo componente.  
  
-   0 para todos os outros tipos de dados.  
  
 Para todos os tipos de dados de intervalo, o campo descritor de SQL_DESC_DATETIME_INTERVAL_PRECISION, que contém a precisão de campo de intervalo à esquerda, é definido como um valor padrão de 2.  
  
 Quando o campo de SQL_DESC_TYPE em um APD é definido como um tipo de data/hora ou de intervalo C, chamando **SQLBindParameter** ou **SQLSetDescField**, os campos SQL_DESC_PRECISION e SQL_DESC_DATETIME_INTERVAL_PRECISION no APD são definidos como o padrão fornecido anteriormente. Isso é verdadeiro para parâmetros de entrada, mas não para parâmetros de entrada/saída ou saída.  
  
 Uma chamada para **SQLSetDescRec** define a precisão inicial do intervalo para o padrão, mas define a precisão do intervalo em segundos (no campo SQL_DESC_PRECISION) com o valor de seu argumento de *precisão* .  
  
 Se qualquer um dos padrões fornecidos anteriormente não for aceitável para um aplicativo, o aplicativo deverá definir o SQL_DESC_PRECISION ou SQL_DESC_DATETIME_INTERVAL_PRECISION campo chamando **SQLSetDescField**.  
  
 Se o aplicativo chamar **SQLGetData** para retornar dados em um tipo de data/hora ou de intervalo C, a precisão do intervalo padrão de precisão e intervalo de segundos será usada. Se o padrão não for aceitável, o aplicativo deverá chamar **SQLSetDescField** para definir o campo de descritor ou **SQLSetDescRec** para definir SQL_DESC_PRECISION. A chamada para **SQLGetData** deve ter um *TargetType* de SQL_ARD_TYPE para usar os valores nos campos de descritor.  
  
 Quando **SQLPutData** é chamado, a precisão dos segundos de precisão e intervalo de intervalo é lida nos campos do registro do descritor que correspondem à coluna ou ao parâmetro de dados em execução, que são campos APD para chamadas para campos **SQLExecute** ou **SQLExecDirect**ou ARD para chamadas para **SQLBulkOperations** ou **SQLSetPos**.
