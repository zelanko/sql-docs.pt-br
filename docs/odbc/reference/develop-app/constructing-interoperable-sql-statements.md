---
title: Construindo instruções SQL interoperáveis | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc8072a6d7291a546f0f12256aa4b336da037a83
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281087"
---
# <a name="constructing-interoperable-sql-statements"></a>Construir instruções SQL interoperáveis
Conforme mencionado nas seções anteriores, os aplicativos interoperáveis devem usar a gramática SQL ODBC. Além de usar esta gramática, no entanto, uma série de problemas adicionais enfrentada por aplicativos interoperáveis. Por exemplo, o que um aplicativo faz se desejar usar um recurso, como junções externas, que não é suportado por todas as fontes de dados?  
  
 Neste ponto, o criador do aplicativo deve tomar algumas decisões sobre quais recursos de idioma são necessários e opcionais. Na maioria dos casos, se um determinado driver não dá suporte a um recurso exigido pelo aplicativo, o aplicativo simplesmente se recusar a executar com esse driver. No entanto, se o recurso é opcional, o aplicativo pode contornar o recurso. Por exemplo, ele pode desabilitar essas partes da interface que permitem ao usuário usar o recurso.  
  
 Para determinar quais recursos têm suporte, os aplicativos iniciam chamando **SQLGetInfo** com a opção SQL_SQL_CONFORMANCE. O nível de compatibilidade do SQL oferece ao aplicativo uma visão geral dos quais há suporte para SQL. Para refinar essa exibição, o aplicativo chama **SQLGetInfo** com qualquer uma das várias outras opções. Para obter uma lista completa dessas opções, consulte o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função. Por fim, **SQLGetTypeInfo** retorna informações sobre os tipos de dados com suporte pela fonte de dados. As seções a seguir listam uma série de fatores possíveis que aplicativos devem ter cuidado ao construir as instruções de SQL interoperáveis.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Catálogo e o uso do esquema](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [Posição de catálogo](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [Identificadores entre aspas](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [Caso do identificador](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [Sequências de escape](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [Prefixos e sufixos de literais](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [Marcadores de parâmetro em chamadas de procedimento](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [Instruções DDL](../../../odbc/reference/develop-app/ddl-statements.md)
