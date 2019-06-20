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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22271cd37069123d0e11a3d0ab660134c61e283b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224463"
---
# <a name="column-size"></a>Tamanho da coluna
O tamanho de coluna (ou parâmetro) dos tipos de dados numéricos é definido como o número máximo de dígitos usado pelo tipo de dados da coluna ou parâmetro ou a precisão dos dados. Para tipos de caractere, esse é o comprimento em caracteres de dados; para tipos de dados binários, o tamanho da coluna é definido como o comprimento em bytes dos dados. Para o tempo, carimbo de hora e todos os tipos de dados de intervalo, isso é o número de caracteres na representação de caracteres de dados. O tamanho da coluna definido para cada tipo de dados SQL conciso é mostrado na tabela a seguir.  
  
|Identificador de tipo SQL|Tamanho da coluna|  
|-------------------------|-----------------|  
|Todos os tipos de caracteres [a] [b].|O tamanho da coluna definido ou máximo em caracteres da coluna ou parâmetro (como contido no campo de descritor SQL_DESC_LENGTH). Por exemplo, o tamanho da coluna de uma coluna de caractere de byte único definido como CHAR(10) é 10.|  
|SQL_DECIMAL SQL_NUMERIC|O número definido de dígitos. Por exemplo, a precisão de uma coluna definida como NUMERIC(10,3) é 10.|  
|SQL_BIT[c]|1|  
|SQL_TINYINT[c]|3|  
|SQL_SMALLINT[c]|5|  
|SQL_INTEGER[c]|10|  
|SQL_BIGINT[c]|19 (se tiver sinal) ou 20 (se não tiver sinal)|  
|SQL_REAL[c]|7|  
|SQL_FLOAT[c]|15|  
|SQL_DOUBLE[c]|15|  
|Todos os tipos binários [a] [b].|O definido ou máximo comprimento em bytes da coluna ou parâmetro. Por exemplo, o comprimento de uma coluna definida como binário (10) é 10.|  
|SQL_TYPE_DATE[c]|10 (o número de caracteres a *aaaa-mm-dd* formato).|  
|SQL_TYPE_TIME[c]|8 (o número de caracteres na *hh-mm-ss* formato), ou 9 + *s* (o número de caracteres no *hh*formato [.... fff], onde *s*é a precisão de segundos).|  
|SQL_TYPE_TIMESTAMP|16 (o número de caracteres a *aaaa-mm-dd hh* formato)<br /><br /> 19 (o número de caracteres a *aaaa-mm-dd* *hh* formato)<br /><br /> ou em<br /><br /> 20 + *s* (o número de caracteres a *aaaa-mm-dd hh*formato [.... fff], onde *s* é a precisão de segundos).|  
|SQL_INTERVAL_SECOND|Em que *p* é o intervalo de precisão inicial e *s* é a precisão de segundos *p* (se *s*= 0) ou *p* + *s*+ 1 (se *s*> 0). [ 1!d]|  
|SQL_INTERVAL_DAY_TO_SECOND|Em que *p* é o intervalo de precisão inicial e *s* é a precisão de segundos, 9 +*p* (se *s*= 0) ou 10 +*p* + *s* (se *s*> 0). [ 1!d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|Em que *p* é o intervalo de precisão inicial e *s* é a precisão de segundos, 6 +*p* (se *s*= 0) ou 7 +*p* + *s* (se *s*> 0). [ 1!d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|Em que *p* é o intervalo de precisão inicial e *s* é a precisão de segundos, 3 ou superior*p* (se *s*= 0) ou 4 +*p* + *s* (se *s*> 0). [ 1!d]|  
|SQL_INTERVAL_YEAR  SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*, onde *p* é o intervalo de precisão inicial. [ 1!d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*, onde *p* é o intervalo de precisão inicial. [ 1!d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*, onde *p* é o intervalo de precisão inicial. [ 1!d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*, onde *p* é o intervalo de precisão inicial. [ 1!d]|  
|SQL_GUID|36 (o número de caracteres a *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* formato)|  
  
 [a] para o ODBC 1.0 em um aplicativo que chama **SQLSetParam** um driver ODBC 2.0 e, para uma aplicativo ODBC 2.0 que chama **SQLBindParameter** em um driver ODBC 1.0, quando \*  *StrLen_or_IndPtr* SQL_DATA_AT_EXEC destina-se um tipo de SQL_LONGVARCHAR ou SQL_LONGVARBINARY *ColumnSize* deve ser definida como o comprimento total dos dados a serem enviados, não a precisão conforme definido nesta tabela.  
  
 [b] se o driver não puder determinar o comprimento de coluna ou parâmetro para um tipo de variável, ele retornará SQL_NO_TOTAL.  
  
 [c] quanto *ColumnSize* argumento de **SQLBindParameter** é ignorado para este tipo de dados.  
  
 [d] para regras gerais sobre o tamanho de coluna em tipos de dados de intervalo, consulte [comprimento do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md), anteriormente neste apêndice.  
  
 Os valores retornados para o tamanho da coluna (ou parâmetro) não correspondem aos valores em um campo de descritor. Os valores podem vir do SQL_DESC_PRECISION ou o campo SQL_DESC_LENGTH, dependendo do tipo de dados, conforme mostrado na tabela a seguir.  
  
|Tipo SQL|Campo de descritor correspondente<br /><br /> tamanho de coluna ou parâmetro|  
|--------------|--------------------------------------------------------------------|  
|Todos os caracteres e tipos binários|LENGTH|  
|Todos os tipos numéricos|PRECISION|  
|Todos os tipos de data e hora e intervalo|LENGTH|  
|SQL_BIT|LENGTH|
