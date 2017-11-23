---
title: "Níveis de conformidade do SQL | Microsoft Docs"
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
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a493a53b736ef5a2606cca1fca710957e30616f1
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sql-conformance-levels"></a>Níveis de conformidade do SQL
O nível de suporte por um driver de gramática de SQL-92 é indicado pelo valor retornado por uma chamada para **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Indica se o driver está de acordo com os níveis de entrada, transição de FIPS, intermediário ou completo definidos em SQL-92.  
  
 Todos os drivers ODBC devem oferecer suporte a gramática SQL mínima descrita em [gramática de SQL mínima](../../../odbc/reference/appendixes/sql-minimum-grammar.md) na gramática do apêndice c: SQL. Esta gramática é um subconjunto do nível de entrada do SQL-92. Drivers podem oferecer suporte ao SQL adicional e ser compatível para o nível de entrada do SQL-92, intermediário ou completo ou o FIPS 127-2 nível de transição. Os drivers compatíveis para um determinado nível de SQL-92 ou FIPS 127-2 podem oferecer suporte a recursos adicionais em qualquer um dos níveis mais altos ainda não estar totalmente em conformidade com esse nível. Para determinar se há suporte para um recurso, um aplicativo deve chamar **SQLGetInfo** com o tipo de informações apropriadas. O nível de conformidade de um recurso do SQL é descrito no tipo de informações correspondentes. (Consulte o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.)

