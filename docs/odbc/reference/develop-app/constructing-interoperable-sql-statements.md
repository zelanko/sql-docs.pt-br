---
title: "Construindo instruções SQL interoperável | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 070b42e5350471ec86fbc256f2005dd7c0385002
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="constructing-interoperable-sql-statements"></a>Construindo instruções SQL interoperáveis
Conforme mencionado na seção anterior, os aplicativos interoperáveis devem usar a gramática SQL ODBC. Além de usar esta gramática, no entanto, um número de problemas adicionais é enfrentado pelos aplicativos interoperáveis. Por exemplo, o que um aplicativo faz se desejar usar um recurso, como junções externas, que não é suportado por todas as fontes de dados?  
  
 Neste ponto, o gravador de aplicativos deve tomar algumas decisões sobre quais recursos de idioma são necessários e opcionais. Na maioria dos casos, se um driver específico não dá suporte a um recurso exigido pelo aplicativo, o aplicativo simplesmente se recusa a executar com esse driver. No entanto, se o recurso é opcional, o aplicativo pode resolver o recurso. Por exemplo, ele pode desabilitar as partes da interface que permite que o usuário use o recurso.  
  
 Para determinar quais recursos têm suporte, os aplicativos iniciam chamando **SQLGetInfo** com a opção SQL_SQL_CONFORMANCE. O nível de conformidade do SQL dá ao aplicativo uma visão geral dos quais há suporte para SQL. Para refinar nessa exibição, o aplicativo chama **SQLGetInfo** com qualquer uma das várias outras opções. Para obter uma lista completa dessas opções, consulte o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função. Por fim, **SQLGetTypeInfo** retorna informações sobre os tipos de dados suportados pela fonte de dados. As seções a seguir listam alguns possíveis fatores de aplicativos devem ter cuidado ao construir interoperáveis instruções de SQL.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Catálogo e o uso do esquema](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [Posição de catálogo](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [Identificadores entre aspas](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [Caso do identificador](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [Sequências de escape](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [Prefixos e sufixos de literais](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [Marcadores de parâmetro em chamadas de procedimento](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [Instruções DDL](../../../odbc/reference/develop-app/ddl-statements.md)

