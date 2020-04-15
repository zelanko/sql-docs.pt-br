---
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
ms.openlocfilehash: 07b6151c723cb5e05189791100338e9e343c28aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306577"
---
# <a name="column-size"></a>Tamanho da coluna
O tamanho da coluna (ou parâmetro) dos tipos de dados numéricos é definido como o número máximo de dígitos usados pelo tipo de dados da coluna ou parâmetro, ou a precisão dos dados. Para tipos de caracteres, este é o comprimento nos caracteres dos dados; para tipos de dados binários, o tamanho da coluna é definido como o comprimento em bytes dos dados. Para o tempo, carimbo de tempo e todos os tipos de dados de intervalo, este é o número de caracteres na representação de caracteres desses dados. O tamanho da coluna definido para cada tipo de dados SQL conciso é mostrado na tabela a seguir.  
  
|Identificador tipo SQL|Tamanho da coluna|  
|-------------------------|-----------------|  
|Todos os tipos de caracteres[a],[b]|O tamanho da coluna definido ou máximo em caracteres da coluna ou parâmetro (conforme contido no campo descritor SQL_DESC_LENGTH). Por exemplo, o tamanho da coluna de uma coluna de caracteres de byte único definida como CHAR(10) é de 10.|  
|SQL_DECIMAL SQL_NUMERIC|O número definido de dígitos. Por exemplo, a precisão de uma coluna definida como NUMERIC(10,3) é de 10.|  
|SQL_BIT[c]|1|  
|SQL_TINYINT[c]|3|  
|SQL_SMALLINT[c]|5|  
|SQL_INTEGER[c]|10|  
|SQL_BIGINT[c]|19 (se assinado) ou 20 (se não assinado)|  
|SQL_REAL[c]|7|  
|SQL_FLOAT[c]|15|  
|SQL_DOUBLE[c]|15|  
|Todos os tipos binários[a],[b]|O comprimento definido ou máximo em bytes da coluna ou parâmetro. Por exemplo, o comprimento de uma coluna definida como BINARY(10) é de 10.|  
|SQL_TYPE_DATE[c]|10 (o número de caracteres no formato *yyyy-mm-dd).*|  
|SQL_TYPE_TIME[c]|8 (o número de caracteres no formato *hh-mm-ss),* ou 9 + *s* (o número de caracteres no formato *hh:mm:ss*[.fff...], onde *s* é a precisão dos segundos).|  
|SQL_TYPE_TIMESTAMP|16 (o número de caracteres no formato *yyyy-mm-dd hh:mm)*<br /><br /> 19 (o número de caracteres no formato *yyyy-mm-dd* *hh:mm:ss)*<br /><br /> ou<br /><br /> 20 + *s* (o número de caracteres no formato *yyyy-mm-dd hh:mm:ss*[.fff...], onde *s* é a precisão dos segundos).|  
|SQL_INTERVAL_SECOND|Quando *p* é o intervalo de precisão líder e *s* é a precisão segundos, *p* (se *s*=0) ou *p*+*s*+1 (se *s*>0). [d]|  
|SQL_INTERVAL_DAY_TO_SECOND|Onde *p* é o intervalo de precisão líder e *s* é a precisão segundos, 9+*p* (se *s*=0) ou 10+*p*+*s* (se *s*>0). [d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|Onde *p* é o intervalo de precisão líder e *s* é a precisão segundos, 6+*p* (se *s*=0) ou 7+*p*+*s* (se *s*>0). [d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|Onde *p* é o intervalo de precisão líder e *s* é a precisão segundos, 3+*p* (se *s*=0) ou 4+*p*+*s* (se *s*>0). [d]|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*, onde *p* é o intervalo de precisão de liderança. [d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3+*p*, onde *p* é o intervalo de precisão de liderança. [d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6+*p*, onde *p* é o intervalo de precisão de liderança. [d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3+*p*, onde *p* é o intervalo de precisão de liderança. [d]|  
|SQL_GUID|36 (o número de caracteres no formato *aaaaaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee*|  
  
 [a] Para um aplicativo ODBC 1.0 chamado **SQLSetParam** em um driver ODBC 2.0 e para um aplicativo ODBC 2.0 \*chamando **SQLBindParameter** em um driver ODBC 1.0, quando *StrLen_or_IndPtr* é SQL_DATA_AT_EXEC para um SQL_LONGVARCHAR ou SQL_LONGVARBINARY tipo, O Tamanho da *Coluna* deve ser definido para o comprimento total dos dados a serem enviados, não a precisão como definido nesta tabela.  
  
 [b] Se o driver não puder determinar a coluna ou o comprimento do parâmetro para um tipo variável, ele retorna SQL_NO_TOTAL.  
  
 [c] O argumento *ColumnSize* do **SQLBindParameter** é ignorado para este tipo de dados.  
  
 [d] Para obter regras gerais sobre o comprimento da coluna nos tipos de dados de intervalo, consulte [Interval Data Type Length](../../../odbc/reference/appendixes/interval-data-type-length.md), anteriormente neste apêndice.  
  
 Os valores retornados para o tamanho da coluna (ou parâmetro) não correspondem aos valores em qualquer campo descritor. Os valores podem vir tanto do SQL_DESC_PRECISION quanto do campo SQL_DESC_LENGTH, dependendo do tipo de dados, conforme mostrado na tabela a seguir.  
  
|Tipo SQL|Campo descritor correspondente a<br /><br /> tamanho da coluna ou parâmetro|  
|--------------|--------------------------------------------------------------------|  
|Todos os tipos de caracteres e binários|LENGTH|  
|Todos os tipos numéricos|PRECISION|  
|Todos os tipos de data e intervalo|LENGTH|  
|SQL_BIT|LENGTH|
