---
title: Conjunto de resultados de SQLGetTypeInfo exemplo | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL data types [ODBC], examples
- SQLGetTypeInfo function [ODBC], examples
- data types [ODBC], SQL data types
ms.assetid: dc1952cc-7581-4d69-9c72-7dc1cd370836
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0953a2a8de3dce18d404929ee23d054192a2e3e7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="example-sqlgettypeinfo-result-set"></a>Conjunto de resultados de SQLGetTypeInfo de exemplo
Um aplicativo chama **SQLGetTypeInfo** para determinar quais tipos de dados têm suporte por uma fonte de dados e as características desses tipos de dados. As tabelas a seguir mostram um conjunto de resultados de exemplo retornado por **SQLGetTypeInfo** para uma fonte de dados que oferece suporte a SQL_CHAR, SQL_LONGVARCHAR, SQL_DECIMAL, SQL_REAL, SQL_DATETIME, SQL_INTERVAL_YEAR e SQL_INTERVAL_DAY_TO_SECOND.  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|"char"|SQL_CHAR|255|"'"|"'"|"comprimento"|SQL_TRUE|  
|"texto"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<Nulo >|SQL_TRUE|  
|"decimal"|SQL_DECIMAL|28|\<Nulo >|\<Nulo >|"precisão,<br />escala"|SQL_TRUE|  
|"real"|SQL_REAL|7|\<Nulo >|\<Nulo >|\<Nulo >|SQL_TRUE|  
|"datetime"|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<Nulo >|SQL_TRUE|  
|"INTERVALO YEAR() ANO"|SQL_INTERVAL_YEAR|9|"'"|"'"|"precisão"|SQL_TRUE|  
|"INTERVALO DAY() PARA FRACTION(5)"|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|"precisão"|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|SEARCHABLE|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<Nulo >|SQL_FALSE|\<Nulo >|"char"|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<Nulo >|SQL_FALSE|\<Nulo >|"texto"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"decimal"|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"real"|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<Nulo >|SQL_FALSE|\<Nulo >|"datetime"|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<Nulo >|SQL_FALSE|\<Nulo >|"INTERVALO YEAR() ANO"|  
TERVAL_DAY_TO_SECOND * *|SQL_FALSE|SQL_PRED_BASIC|\<Nulo >|SQL_FALSE|\<Nulo >|"INTERVALO DAY() PARA FRACTION(5)"|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<Nulo >|\<Nulo >|SQL_CHAR|\<Nulo >|\<Nulo >|\<Nulo >|  
|**SQL_LONGVARCHAR**|\<Nulo >|\<Nulo >|SQL_LONGVARCHAR|\<Nulo >|\<Nulo >|\<Nulo >|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<Nulo >|10|\<Nulo >|  
|**SQL_REAL**|\<Nulo >|\<Nulo >|SQL_REAL|\<Nulo >|10|\<Nulo >|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<Nulo >|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<Nulo >|9|  
ERVAL_DAY_TO_SECOND * *|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<Nulo >|9|
