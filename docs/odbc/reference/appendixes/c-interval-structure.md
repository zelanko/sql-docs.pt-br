---
title: Estrutura de intervalo de C | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a2af7ec87b34ba6b2a8482d9321905f409dd9dd3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="c-interval-structure"></a>Estrutura de intervalo de C
Cada um dos tipos de dados C intervalo listado no [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) seção usa a mesma estrutura para conter os dados de intervalo. Quando **SQLFetch**, **SQLFetchScroll**, ou **SQLGetData** é chamado, o driver retorna dados na estrutura de SQL_INTERVAL_STRUCT, usa o valor especificado pelo para os tipos de dados C (na chamada para **SQLBindCol**, **SQLGetData**, ou **SQLBindParameter**) para interpretar o conteúdo de SQL_INTERVAL_STRUCT e preenche o *interval_type* campo da estrutura com a *enum* valor correspondente ao tipo de C. Observe que os drivers não lê o *interval_type* campo para determinar o tipo do intervalo; eles recuperarem o valor do campo de descritor SQL_DESC_CONCISE_TYPE. Quando a estrutura é usada para dados de parâmetro, o driver usa o valor especificado pelo aplicativo no campo SQL_DESC_CONCISE_TYPE de APD para interpretar o conteúdo de SQL_INTERVAL_STRUCT, mesmo que o aplicativo define o valor da  *interval_type* campo para um valor diferente.  
  
 Essa estrutura é definida da seguinte maneira:  
  
```  
typedef struct tagSQL_INTERVAL_STRUCT  
{  
   SQLINTERVAL interval_type;   
   SQLSMALLINT interval_sign;  
   union {  
         SQL_YEAR_MONTH_STRUCT   year_month;  
         SQL_DAY_SECOND_STRUCT   day_second;  
         } intval;  
} SQL_INTERVAL_STRUCT;  
typedef enum   
{  
   SQL_IS_YEAR = 1,  
   SQL_IS_MONTH = 2,  
   SQL_IS_DAY = 3,  
   SQL_IS_HOUR = 4,  
   SQL_IS_MINUTE = 5,  
   SQL_IS_SECOND = 6,  
   SQL_IS_YEAR_TO_MONTH = 7,  
   SQL_IS_DAY_TO_HOUR = 8,  
   SQL_IS_DAY_TO_MINUTE = 9,  
   SQL_IS_DAY_TO_SECOND = 10,  
   SQL_IS_HOUR_TO_MINUTE = 11,  
   SQL_IS_HOUR_TO_SECOND = 12,  
   SQL_IS_MINUTE_TO_SECOND = 13  
} SQLINTERVAL;  
  
typedef struct tagSQL_YEAR_MONTH  
{  
   SQLUINTEGER year;  
   SQLUINTEGER month;   
} SQL_YEAR_MONTH_STRUCT;  
  
typedef struct tagSQL_DAY_SECOND  
{  
   SQLUINTEGER day;  
   SQLUINTEGER hour;  
   SQLUINTEGER minute;  
   SQLUINTEGER second;  
   SQLUINTEGER fraction;  
} SQL_DAY_SECOND_STRUCT;  
```  
  
 O *interval_type* campo do SQL_INTERVAL_STRUCT indica para o aplicativo que estrutura é mantida na união e também quais membros da estrutura são relevantes. O *interval_sign* campo tem o valor SQL_FALSE se o intervalo à esquerda de campo não está assinado; se for SQL_TRUE, o campo principal é negativo. O valor no campo à esquerda em si é sempre não assinado, independentemente do valor *interval_sign*. O *interval_sign* campo atua como um bit de sinal.
