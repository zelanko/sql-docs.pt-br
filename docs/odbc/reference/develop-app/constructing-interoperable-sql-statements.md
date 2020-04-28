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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1eccdef63b7d06a456a07f5f1a9ccad987d2de29
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282506"
---
# <a name="constructing-interoperable-sql-statements"></a>Construir instruções SQL interoperáveis
Conforme mencionado nas seções anteriores, os aplicativos interoperáveis devem usar a gramática do SQL ODBC. No entanto, além de usar essa gramática, vários problemas adicionais são enfrentados por aplicativos interoperáveis. Por exemplo, o que um aplicativo faz se quiser usar um recurso, como junções externas, que não tem suporte de todas as fontes de dados?  
  
 Neste ponto, o gravador de aplicativos deve tomar algumas decisões sobre quais recursos de idioma são necessários e quais são opcionais. Na maioria dos casos, se um driver específico não oferecer suporte a um recurso exigido pelo aplicativo, o aplicativo simplesmente se recusará a ser executado com esse driver. No entanto, se o recurso for opcional, o aplicativo poderá contornar o recurso. Por exemplo, ele pode desabilitar essas partes da interface que permitem ao usuário usar o recurso.  
  
 Para determinar quais recursos têm suporte, os aplicativos começam chamando **SQLGetInfo** com a opção SQL_SQL_CONFORMANCE. O nível de conformidade do SQL fornece ao aplicativo uma visão ampla da qual há suporte para SQL. Para refinar essa exibição, o aplicativo chama **SQLGetInfo** com uma série de outras opções. Para obter uma lista completa dessas opções, consulte a descrição da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) . Por fim, **SQLGetTypeInfo** retorna informações sobre os tipos de dados com suporte pela fonte de dados. As seções a seguir listam vários dos possíveis fatores que os aplicativos devem observar ao construir instruções SQL interoperáveis.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Catálogo e o uso do esquema](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [Posição de catálogo](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [Identificadores entre aspas](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [Caso do identificador](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [Sequências de escape](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [Prefixos e sufixos de literais](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [Marcadores de parâmetro em chamadas de procedimento](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [Instruções DDL](../../../odbc/reference/develop-app/ddl-statements.md)
