---
title: Função CAST do SQL-92 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09d2a2de710dafd4e744166c4219f4c903fd3321
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305057"
---
# <a name="sql-92-cast-function"></a>Função CAST do SQL-92
A função **Cast** definida em SQL-92 é equivalente à função **Convert** definida em ODBC. A sintaxe das funções equivalentes é a seguinte:  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 A função **Cast** do SQL-92 exige quais tipos de dados podem ser convertidos em quais outros tipos de dados. (Para obter mais informações, consulte a especificação do SQL-92.) A função **Cast** tem suporte no nível de transição FIPS.  
  
 Um aplicativo pode determinar o suporte para a função **Cast** da seguinte maneira:  
  
1.  Chame **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Se o valor de retorno para o tipo de informação for SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE ou SQL_SC_SQL92_FULL, a função **Cast** terá suporte.  
  
2.  Se o valor de retorno do tipo de informação SQL_SQL_CONFORMANCE for SQL_SC_ENTRY_LEVEL ou 0, chame **SQLGetInfo** com o tipo de informações SQL_SQL92_VALUE_EXPRESSIONS. Se o bit de SQL_SVE_CAST for definido, a função **Cast** terá suporte.
