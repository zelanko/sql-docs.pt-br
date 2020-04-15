---
title: Níveis de conformidade SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 875330ac78588566b4b1c212f7a65d2841127a61
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301377"
---
# <a name="sql-conformance-levels"></a>Níveis de conformidade SQL
O nível de gramática SQL-92 suportado por um driver é indicado pelo valor retornado por uma chamada ao **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Isso indica se o driver está de acordo com os níveis de Entrada, Transitório FIPS, Intermediário ou Completo definidos no SQL-92.  
  
 Todos os drivers ODBC devem suportar a gramática SQL mínima descrita na [Gramática Mínima SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) no apêndice C: Gramática SQL. Esta gramática é um subconjunto do nível de entrada do SQL-92. Os drivers podem suportar SQL adicional e estar em conformidade com o nível de entrada, intermediário ou completo do SQL-92, ou com o nível de transição FIPS 127-2. Os drivers que cumprem um determinado nível de SQL-92 ou FIPS 127-2 podem suportar recursos adicionais em qualquer um dos níveis mais altos, mas ainda não estar totalmente conformado a esse nível. Para determinar se um recurso é suportado, um aplicativo deve ligar para **o SQLGetInfo** com o tipo de informação apropriado. O nível de conformidade de um recurso SQL é descrito no tipo de informação correspondente. (Veja a descrição da função [SQLGetInfo.)](../../../odbc/reference/syntax/sqlgetinfo-function.md)
