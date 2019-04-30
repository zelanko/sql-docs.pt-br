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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db5077b9df2673593b6eaec9622aafd1d2c77234
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270627"
---
# <a name="sql-92-cast-function"></a>Função CAST do SQL-92
O **CAST** função definida no SQL-92 é equivalente ao **converter** função definida no ODBC. A sintaxe das funções equivalentes é da seguinte maneira:  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 O SQL-92 **CAST** função determina quais tipos de dados podem ser convertidos em quais outros tipos de dados. (Para obter mais informações, consulte a especificação SQL-92). O **CAST** há suporte para a função no nível de transição de FIPS.  
  
 Um aplicativo pode determinar se há suporte para o **CAST** funcionam da seguinte maneira:  
  
1.  Chame **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Se o valor retornado para o tipo de informação é SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE ou SQL_SC_SQL92_FULL, o **CAST** suporte para a função.  
  
2.  Se o valor de retorno do tipo de informações SQL_SQL_CONFORMANCE estiver SQL_SC_ENTRY_LEVEL ou 0, chame **SQLGetInfo** com o tipo de informação SQL_SQL92_VALUE_EXPRESSIONS. Se o bit SQL_SVE_CAST for definido, o **CAST** suporte para a função.
