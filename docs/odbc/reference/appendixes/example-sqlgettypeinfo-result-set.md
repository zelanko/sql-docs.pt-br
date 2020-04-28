---
title: Conjunto de resultados SQLGetTypeInfo de exemplo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], examples
- SQLGetTypeInfo function [ODBC], examples
- data types [ODBC], SQL data types
ms.assetid: dc1952cc-7581-4d69-9c72-7dc1cd370836
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5cf62f8a95f4c91095c21a6d603317fe1f73500
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307007"
---
# <a name="example-sqlgettypeinfo-result-set"></a>Conjunto de resultados SQLGetTypeInfo de exemplo
Um aplicativo chama **SQLGetTypeInfo** para determinar quais tipos de dados têm suporte de uma fonte de dados e as características desses tipos de dados. As tabelas a seguir mostram um conjunto de resultados de exemplo retornado por **SQLGetTypeInfo** para uma fonte de dados que dá suporte a SQL_CHAR, SQL_LONGVARCHAR, SQL_DECIMAL, SQL_REAL, SQL_DATETIME, SQL_INTERVAL_YEAR e SQL_INTERVAL_DAY_TO_SECOND.  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|º|SQL_CHAR|255|"'"|"'"|muito|SQL_TRUE|  
|"texto"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<> nulo|SQL_TRUE|  
|vírgula|SQL_DECIMAL|28|\<> nulo|\<> nulo|Preciso<br />escalonáve|SQL_TRUE|  
|foto|SQL_REAL|7|\<> nulo|\<> nulo|\<> nulo|SQL_TRUE|  
|horário|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<> nulo|SQL_TRUE|  
|"ANO DE INTERVALO () PARA ANO"|SQL_INTERVAL_YEAR|9|"'"|"'"|Preciso|SQL_TRUE|  
|"INTERVAL DAY () TO FRACIONÁRIO (5)"|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|Preciso|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|SEARCHABLE|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<> nulo|SQL_FALSE|\<> nulo|º|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<> nulo|SQL_FALSE|\<> nulo|"texto"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|vírgula|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|foto|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<> nulo|SQL_FALSE|\<> nulo|horário|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<> nulo|SQL_FALSE|\<> nulo|"ANO DE INTERVALO () PARA ANO"|  
|**SQL_INTERVAL_DAY_TO_SECOND**|SQL_FALSE|SQL_PRED_BASIC|\<> nulo|SQL_FALSE|\<> nulo|"INTERVAL DAY () TO FRACIONÁRIO (5)"|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<> nulo|\<> nulo|SQL_CHAR|\<> nulo|\<> nulo|\<> nulo|  
|**SQL_LONGVARCHAR**|\<> nulo|\<> nulo|SQL_LONGVARCHAR|\<> nulo|\<> nulo|\<> nulo|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<> nulo|10|\<> nulo|  
|**SQL_REAL**|\<> nulo|\<> nulo|SQL_REAL|\<> nulo|10|\<> nulo|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<> nulo|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<> nulo|9|  
|**SQL_INTERVAL_DAY_TO_SECOND**|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<> nulo|9|
