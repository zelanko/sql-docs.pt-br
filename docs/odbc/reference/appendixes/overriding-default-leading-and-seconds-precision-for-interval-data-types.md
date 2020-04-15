---
title: Substituir a precisão de líderes e segundos para tipos de dados de intervalo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e60d5d8fc696ad8e2bd4cfb0c082ff214e066d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303597"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>Substituir precisão inicial e de segundos padrão para tipos de dados de intervalo
Quando o campo SQL_DESC_TYPE de um ARD é definido como um tipo de data ou intervalo C, chamando **sqlBindCol** ou **SQLSetDescField,** o campo SQL_DESC_PRECISION (que contém a precisão dos segundos de intervalo) é definido para os seguintes padrões:  
  
-   6 para carimbo de tempo e todos os tipos de dados de intervalo com um segundo componente.  
  
-   0 para todos os outros tipos de dados.  
  
 Para todos os tipos de dados de intervalo, o campo descritor SQL_DESC_DATETIME_INTERVAL_PRECISION, que contém a precisão do campo de campo líder do intervalo, é definido como um valor padrão de 2.  
  
 Quando o campo de SQL_DESC_TYPE em uma APD é definido como um tipo de data ou intervalo C, chamando **sqlBindParameter** ou **SQLSetDescField,** os campos SQL_DESC_PRECISION e SQL_DESC_DATETIME_INTERVAL_PRECISION na APD são definidos como padrão dado anteriormente. Isso é verdadeiro para parâmetros de entrada, mas não para parâmetros de entrada/saída ou de saída.  
  
 Uma chamada para **SQLSetDescRec** define o intervalo que leva a precisão ao padrão, mas define a precisão dos segundos de intervalo (no campo SQL_DESC_PRECISION) para o valor de seu argumento *Precisão.*  
  
 Se qualquer um dos padrões dado anteriormente não for aceitável para um aplicativo, o aplicativo deverá definir o campo SQL_DESC_PRECISION ou SQL_DESC_DATETIME_INTERVAL_PRECISION ligando para **SQLSetDescField**.  
  
 Se o aplicativo chamar **o SQLGetData** para retornar os dados em um tipo de data ou intervalo C, o intervalo padrão de precisão e precisão de segundos de intervalo será usado. Se qualquer padrão não for aceitável, o aplicativo deve chamar **SQLSetDescField** para definir o campo descritor ou **o SQLSetDescRec** para definir SQL_DESC_PRECISION. A chamada para **SQLGetData** deve ter um *TargetType* de SQL_ARD_TYPE para usar os valores nos campos descritor.  
  
 Quando **o SQLPutData** é chamado, o intervalo de precisão e precisão de segundos de intervalo são lidos nos campos do registro descritor que correspondem ao parâmetro ou coluna data-at-execution, que são campos APD para chamadas para **sqlexecute** ou **sqlexecdirect,** ou campos ARD para chamadas para **SQLBulkOperations** ou **SQLSetPos**.
