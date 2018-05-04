---
title: Tamanho da coluna | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c0f4111b758421dd03be3489e7da82d78e8f181
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="column-size"></a>Tamanho da coluna
O tamanho da coluna (ou parâmetro) dos tipos de dados numérico é definido como o número máximo de dígitos usado pelo tipo de dados da coluna ou parâmetro ou a precisão dos dados. Para tipos de caracteres, esse é o comprimento em caracteres de dados. para tipos de dados binários, o tamanho da coluna é definido como o comprimento em bytes dos dados. Para o tempo, timestamp e todos os tipos de dados de intervalo, este é o número de caracteres a representação de caracteres de dados. O tamanho da coluna definido para cada tipo de dados SQL conciso é mostrado na tabela a seguir.  
  
|Identificador de tipo SQL|Tamanho da coluna|  
|-------------------------|-----------------|  
|Todos os tipos de caracteres [a], [b].|O tamanho da coluna definida ou máximo em caracteres da coluna ou parâmetro (como contida no campo de descritor SQL_DESC_LENGTH). Por exemplo, o tamanho da coluna de uma coluna de caractere de byte único definido como char (10) é 10.|  
|SQL_DECIMAL SQL_NUMERIC|O número definido de dígitos. Por exemplo, a precisão de uma coluna definida como NUMERIC(10,3) é 10.|  
|SQL_BIT [c]|1|  
|SQL_TINYINT [c]|3|  
|SQL_SMALLINT [c]|5|  
|SQL_INTEGER [c]|10|  
|SQL_BIGINT [c]|19 (se conectado) ou 20 (se não assinado)|  
|SQL_REAL [c]|7|  
|SQL_FLOAT [c]|15|  
|SQL_DOUBLE [c]|15|  
|Todos os tipos binários [a], [b].|O definido ou máximo comprimento em bytes da coluna ou parâmetro. Por exemplo, o comprimento de uma coluna definida como binário (10) é 10.|  
|SQL_TYPE_DATE [c]|10 (o número de caracteres a *aaaa-mm-dd* formato).|  
|SQL_TYPE_TIME [c]|8 (o número de caracteres a *hh-mm-ss* formato), 9 + *s* (o número de caracteres a *hh*formato [.... fff], onde *s*é a precisão de segundos).|  
|SQL_TYPE_TIMESTAMP|16 (o número de caracteres a *aaaa-mm-dd hh: mm* formato)<br /><br /> 19 (o número de caracteres a *aaaa-mm-dd* *hh* formato)<br /><br /> ou<br /><br /> 20 + *s* (o número de caracteres a *aaaa-mm-dd hh*formato [.... fff], onde *s* é a precisão de segundos).|  
|SQL_INTERVAL_SECOND|Onde *p* é o intervalo de precisão principal e *s* é a precisão de segundos, *p* (se *s*= 0) ou *p* + *s*+ 1 (se *s*> 0). [ d]|  
|SQL_INTERVAL_DAY_TO_SECOND|Onde *p* é o intervalo de precisão principal e *s* é a precisão de segundos, 9 +*p* (se *s*= 0) ou 10 +*p* + *s* (se *s*> 0). [ d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|Onde *p* é o intervalo de precisão principal e *s* é a precisão de segundos, 6 +*p* (se *s*= 0) ou 7 +*p* + *s* (se *s*> 0). [ d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|Onde *p* é o intervalo de precisão principal e *s* é a precisão de segundos, 3 +*p* (se *s*= 0) ou 4 +*p* + *s* (se *s*> 0). [ d]|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*, onde *p* é o intervalo de precisão principal. [ d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*, onde *p* é o intervalo de precisão principal. [ d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*, onde *p* é o intervalo de precisão principal. [ d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*, onde *p* é o intervalo de precisão principal. [ d]|  
|SQL_GUID|36 (o número de caracteres a *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* formato)|  
  
 [a] para o ODBC 1.0 em um aplicativo que chama **SQLSetParam** em um driver de ODBC 2.0 e para uma aplicativo ODBC 2.0 que chama **SQLBindParameter** em um driver de ODBC 1.0, quando \*  *StrLen_or_IndPtr* é SQL_DATA_AT_EXEC para um tipo SQL_LONGVARCHAR ou SQL_LONGVARBINARY, *ColumnSize* deve ser definida como o comprimento total dos dados a serem enviados, não a precisão conforme definido nesta tabela.  
  
 [b] se o driver não pode determinar o comprimento de coluna ou parâmetro de um tipo de variável, retornará SQL_NO_TOTAL.  
  
 [c] de *ColumnSize* argumento de **SQLBindParameter** é ignorada para esse tipo de dados.  
  
 [d] para regras gerais sobre o comprimento da coluna em tipos de dados de intervalo, consulte [comprimento do intervalo do tipo de dados](../../../odbc/reference/appendixes/interval-data-type-length.md), anteriormente neste apêndice.  
  
 Os valores retornados para o tamanho da coluna (ou parâmetro) não correspondem aos valores em qualquer um campo do descritor. Os valores podem vir do SQL_DESC_PRECISION ou o campo SQL_DESC_LENGTH, dependendo do tipo de dados, conforme mostrado na tabela a seguir.  
  
|Tipo SQL|Campo de descritor correspondente<br /><br /> tamanho de coluna ou parâmetro|  
|--------------|--------------------------------------------------------------------|  
|Todos os caracteres e tipos binários|LENGTH|  
|Todos os tipos numéricos|PRECISION|  
|Todos os tipos de data/hora e intervalo|LENGTH|  
|SQL_BIT|LENGTH|
