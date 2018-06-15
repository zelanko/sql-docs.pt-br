---
title: Função CAST SQL-92 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d7d3d00128d4ddbb79c43f53c0d439e6974ddb6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910931"
---
# <a name="sql-92-cast-function"></a>Função CAST SQL-92
O **CAST** função definida no SQL-92 é equivalente ao **converter** função definida no ODBC. A sintaxe das funções equivalentes é o seguinte:  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 O SQL-92 **CAST** função determina quais tipos de dados podem ser convertidos para que outros tipos de dados. (Para obter mais informações, consulte a especificação de SQL-92). O **CAST** há suporte para a função no nível de transição de FIPS.  
  
 Um aplicativo pode determinar se há suporte para o **CAST** funciona da seguinte maneira:  
  
1.  Chamar **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Se o valor de retorno para o tipo de informações é SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE ou SQL_SC_SQL92_FULL, o **CAST** suporte para a função.  
  
2.  Se o valor de retorno do tipo de informações SQL_SQL_CONFORMANCE é SQL_SC_ENTRY_LEVEL ou 0, chame **SQLGetInfo** com o tipo de informação SQL_SQL92_VALUE_EXPRESSIONS. Se o bit SQL_SVE_CAST for definido, o **CAST** suporte para a função.
