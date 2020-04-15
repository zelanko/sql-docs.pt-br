---
title: Construindo Declarações SQL Interoperáveis | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282506"
---
# <a name="constructing-interoperable-sql-statements"></a>Construir instruções SQL interoperáveis
Como mencionado nas seções anteriores, as aplicações interoperáveis devem usar a gramática ODBC SQL. Além de usar essa gramática, no entanto, uma série de problemas adicionais são enfrentados por aplicações interoperáveis. Por exemplo, o que um aplicativo faz se quiser usar um recurso, como junções externas, que não é suportado por todas as fontes de dados?  
  
 Neste ponto, o autor do aplicativo deve tomar algumas decisões sobre quais características de idioma são necessárias e quais são opcionais. Na maioria dos casos, se um driver em particular não suporta um recurso exigido pelo aplicativo, o aplicativo simplesmente se recusa a correr com esse driver. No entanto, se o recurso for opcional, o aplicativo pode contornar o recurso. Por exemplo, ele pode desativar as partes da interface que permitem ao usuário usar o recurso.  
  
 Para determinar quais recursos são suportados, os aplicativos começam ligando para **o SQLGetInfo** com a opção SQL_SQL_CONFORMANCE. O nível de conformidade SQL dá ao aplicativo uma visão ampla da qual o SQL é suportado. Para refinar essa exibição, o aplicativo chama **SQLGetInfo** com qualquer uma das outras opções. Para obter uma lista completa dessas opções, consulte a descrição da função [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md) Finalmente, **o SQLGetTypeInfo** retorna informações sobre os tipos de dados suportados pela fonte de dados. As seções a seguir listam uma série de fatores possíveis que os aplicativos devem observar ao construir instruções SQL interoperáveis.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Catálogo e o uso do esquema](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [Posição de catálogo](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [Identificadores entre aspas](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [Caso do identificador](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [Sequências de escape](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [Prefixos e sufixos de literais](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [Marcadores de parâmetro em chamadas de procedimento](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [Instruções DDL](../../../odbc/reference/develop-app/ddl-statements.md)
