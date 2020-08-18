---
description: Tamanho da coluna
title: Tamanho da coluna | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53d7934f3ac4669545e3cc24752e4a9e0f4fb589
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411112"
---
# <a name="column-size"></a>Tamanho da coluna
O tamanho da coluna (ou parâmetro) de tipos de dados numéricos é definido como o número máximo de dígitos usados pelo tipo de dados da coluna ou parâmetro, ou a precisão dos dados. Para tipos de caracteres, esse é o comprimento em caracteres dos dados; para tipos de dados Binary, o tamanho da coluna é definido como o comprimento em bytes dos dados. Para o tempo, carimbo de data/hora e todos os tipos de dados de intervalo, este é o número de caracteres na representação de caracteres desses dados. O tamanho da coluna definido para cada tipo de dados SQL conciso é mostrado na tabela a seguir.  
  
|Identificador de tipo SQL|Tamanho da coluna|  
|-------------------------|-----------------|  
|Todos os tipos de caractere [a], [b]|O tamanho de coluna definido ou máximo em caracteres da coluna ou parâmetro (como contido no campo de descritor de SQL_DESC_LENGTH). Por exemplo, o tamanho da coluna de uma coluna de caractere de byte único definido como CHAR (10) é 10.|  
|SQL_DECIMAL SQL_NUMERIC|O número definido de dígitos. Por exemplo, a precisão de uma coluna definida como NUMERIC (10, 3) é 10.|  
|SQL_BIT [c]|1|  
|SQL_TINYINT [c]|3|  
|SQL_SMALLINT [c]|5|  
|SQL_INTEGER [c]|10|  
|SQL_BIGINT [c]|19 (se assinada) ou 20 (se não assinado)|  
|SQL_REAL [c]|7|  
|SQL_FLOAT [c]|15|  
|SQL_DOUBLE [c]|15|  
|Todos os tipos binários [a], [b]|O comprimento definido ou máximo em bytes da coluna ou do parâmetro. Por exemplo, o comprimento de uma coluna definida como BINARY (10) é 10.|  
|SQL_TYPE_DATE [c]|10 (o número de caracteres no formato *aaaa-mm-dd* ).|  
|SQL_TYPE_TIME [c]|8 (o número de caracteres no formato *hh-mm-SS* ) ou 9 + *s* (o número de caracteres no formato *hh: mm: SS*[. FFF...], em que *s* é a precisão de segundos).|  
|SQL_TYPE_TIMESTAMP|16 (o número de caracteres no formato *aaaa-mm-dd hh: mm* )<br /><br /> 19 (o número de caracteres no formato *aaaa-mm-dd* *hh: mm: SS* )<br /><br /> ou<br /><br /> 20 + *s* (o número de caracteres no formato *aaaa-mm-dd hh: mm: SS*[. FFF...], em que *s* é a precisão de segundos).|  
|SQL_INTERVAL_SECOND|Em que *p* é a precisão à esquerda do intervalo e *s* é a precisão de segundos, *p* (se *s*= 0) ou *p* + *s*+ 1 (se *s*>0). [ 3D|  
|SQL_INTERVAL_DAY_TO_SECOND|Em que *p* é a precisão à esquerda do intervalo e *s* é a precisão de segundos, 9 +*p* (se *s*= 0) ou 10 +*p* + *s* (se *s*>0). [ 3D|  
|SQL_INTERVAL_HOUR_TO_SECOND|Em que *p* é a precisão à esquerda do intervalo e *s* é a precisão de segundos, 6 +*p* (se *s*= 0) ou 7 +*p* + *s* (se *s*>0). [ 3D|  
|SQL_INTERVAL_MINUTE_TO_SECOND|Em que *p* é a precisão à esquerda do intervalo e *s* é a precisão de segundos, 3 +*p* (se *s*= 0) ou 4 +*p* + *s* (se *s*>0). [ 3D|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*, em que *p* é a precisão à esquerda do intervalo. 3D|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*, em que *p* é a precisão à esquerda do intervalo. 3D|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*, em que *p* é a precisão à esquerda do intervalo. 3D|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*, em que *p* é a precisão à esquerda do intervalo. 3D|  
|SQL_GUID|36 (o número de caracteres no formato *aaaaaaaa-bbbb-cccc-dddd-EEEEEEEEEEEE* )|  
  
 [a] para um aplicativo ODBC 1,0 chamando **SQLSetParam** em um driver ODBC 2,0 e para um aplicativo ODBC 2,0 chamando **SQLBindParameter** em um driver odbc 1,0, quando \* *StrLen_or_IndPtr* for SQL_DATA_AT_EXEC para um tipo SQL_LONGVARCHAR ou SQL_LONGVARBINARY, *ColumnSize* deve ser definido como o comprimento total dos dados a serem enviados, não a precisão conforme definido nesta tabela.  
  
 [b] se o driver não puder determinar o comprimento da coluna ou do parâmetro para um tipo de variável, ele retornará SQL_NO_TOTAL.  
  
 [c] o argumento *ColumnSize* de **SQLBindParameter** é ignorado para esse tipo de dados.  
  
 [d] para regras gerais sobre o comprimento da coluna em tipos de dados de intervalo, consulte [comprimento do tipo de dados do intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md), anteriormente neste apêndice.  
  
 Os valores retornados para o tamanho da coluna (ou parâmetro) não correspondem aos valores em um campo de descritor. Os valores podem vir do campo SQL_DESC_PRECISION ou SQL_DESC_LENGTH, dependendo do tipo de dados, conforme mostrado na tabela a seguir.  
  
|Tipo SQL|Campo de descritor correspondente a<br /><br /> tamanho da coluna ou do parâmetro|  
|--------------|--------------------------------------------------------------------|  
|Todos os tipos de caracteres e binários|LENGTH|  
|Todos os tipos numéricos|PRECISION|  
|Todos os tipos DateTime e Interval|LENGTH|  
|SQL_BIT|LENGTH|
