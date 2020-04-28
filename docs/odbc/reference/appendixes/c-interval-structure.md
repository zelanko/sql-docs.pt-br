---
title: Estrutura de intervalo de C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02c86ebe24a0e12531e355f95185b01f3089a31b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292148"
---
# <a name="c-interval-structure"></a>Estrutura de intervalo do C
Cada um dos tipos de dados de intervalo de C listados na seção [tipos de dados c](../../../odbc/reference/appendixes/c-data-types.md) usa a mesma estrutura para conter os dados do intervalo. Quando **SQLFetch**, **SQLFetchScroll**ou **SQLGetData** é chamado, o driver retorna dados para a estrutura de SQL_INTERVAL_STRUCT, usa o valor que foi especificado pelo aplicativo para os tipos de dados C (na chamada de **SQLBindCol**, **SQLGetData**ou **SQLBindParameter**) para interpretar o conteúdo de SQL_INTERVAL_STRUCT e popula o campo *interval_type* da estrutura com o valor de *Enumeração* correspondente ao tipo C. Observe que os drivers não lêem o campo *interval_type* para determinar o tipo do intervalo; Eles recuperam o valor do campo descritor de SQL_DESC_CONCISE_TYPE. Quando a estrutura é usada para dados de parâmetro, o driver usa o valor especificado pelo aplicativo no campo SQL_DESC_CONCISE_TYPE do APD para interpretar o conteúdo de SQL_INTERVAL_STRUCT, mesmo que o aplicativo defina o valor do campo *interval_type* para um valor diferente.  
  
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
  
 O campo *interval_type* da SQL_INTERVAL_STRUCT indica para o aplicativo qual estrutura é mantida na União e também quais membros da estrutura são relevantes. O campo *interval_sign* tem o valor SQL_FALSE se o campo à esquerda do intervalo não estiver assinado; Se for SQL_TRUE, o campo à esquerda será negativo. O valor no campo principal é sempre não assinado, independentemente do valor de *interval_sign*. O campo *interval_sign* atua como um bit de sinal.
