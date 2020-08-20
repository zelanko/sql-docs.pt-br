---
description: Níveis de conformidade SQL
title: Níveis de conformidade do SQL | Microsoft Docs
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
ms.openlocfilehash: 525cda9094213e6decf30643c23a7db623511e14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499799"
---
# <a name="sql-conformance-levels"></a>Níveis de conformidade SQL
O nível de gramática do SQL-92 com suporte de um driver é indicado pelo valor retornado por uma chamada para **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Isso indica se o driver está em conformidade com os níveis de entrada, de transição FIPS, intermediário ou completo definidos no SQL-92.  
  
 Todos os drivers ODBC devem oferecer suporte à gramática SQL mínima descrita na [gramática mínima do SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) no Apêndice C: gramática SQL. Essa gramática é um subconjunto do nível de entrada do SQL-92. Os drivers podem dar suporte a SQL adicional e estar em conformidade com o nível de entrada do SQL-92, intermediário ou completo ou para o nível de transição FIPS 127-2. Os drivers que estão em conformidade com um determinado nível de SQL-92 ou FIPS 127-2 podem dar suporte a recursos adicionais em qualquer um dos níveis mais altos, ainda que não estejam totalmente em conformidade com esse nível. Para determinar se há suporte para um recurso, um aplicativo deve chamar **SQLGetInfo** com o tipo de informações apropriado. O nível de conformidade de um recurso SQL é descrito no tipo de informações correspondente. (Consulte a descrição da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .)
