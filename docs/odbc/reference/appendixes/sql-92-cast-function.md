---
title: Função sql-92 CAST | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305057"
---
# <a name="sql-92-cast-function"></a>Função CAST do SQL-92
A função **CAST** definida no SQL-92 é equivalente à função **CONVERT** definida no ODBC. A sintaxe das funções equivalentes é a seguinte:  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 A **função** Cast SQL-92 determina quais tipos de dados podem ser convertidos para quais outros tipos de dados. (Para obter mais informações, consulte a especificação SQL-92.) A função **CAST** é suportada no nível fips transitional.  
  
 Um aplicativo pode determinar o suporte para a função **CAST** da seguinte forma:  
  
1.  Ligue para **o SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Se o valor de retorno para o tipo de informação for SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE ou SQL_SC_SQL92_FULL, a função **CAST** será suportada.  
  
2.  Se o valor de retorno do SQL_SQL_CONFORMANCE tipo de informação for SQL_SC_ENTRY_LEVEL ou 0, ligue para **o SQLGetInfo** com o SQL_SQL92_VALUE_EXPRESSIONS tipo de informação. Se a SQL_SVE_CAST bit estiver definida, a função **CAST** será suportada.
