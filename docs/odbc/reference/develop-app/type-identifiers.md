---
title: Identificadores de tipo | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], identifiers
- type identifiers [ODBC]
- identifiers [ODBC], type
- type identifiers [ODBC], about type identifiers
ms.assetid: 1d9fdfa2-e378-44fe-ac66-9743d9bbdd5a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: da01de66ee5b20d873b3b50ea24c72549174e90b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="type-identifiers"></a>Identificadores de tipo
Para descrever tipos de dados SQL e C, o ODBC define dois conjuntos de *identificadores de tipo*. Um identificador de tipo descreve o tipo de uma coluna SQL ou um buffer de C. É um **#define** valor e é normalmente passado como um argumento de função ou retornados nos metadados.  
  
 Por exemplo, a seguinte chamada para **SQLBindParameter** associa uma variável do tipo SQL_DATE_STRUCT a um parâmetro de data em uma instrução SQL. O identificador de tipo C SQL_C_TYPE_DATE Especifica o tipo do *data* variável e o identificador de tipo SQL SQL_TYPE_DATE Especifica o tipo do parâmetro dinâmico.  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```

