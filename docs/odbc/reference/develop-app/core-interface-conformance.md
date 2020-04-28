---
title: Conformidade da interface principal | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 886ded1cd79b35488c0d47df3dbd8055dc6a8016
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302128"
---
# <a name="core-interface-conformance"></a>Conformidade de interface de núcleo
Todos os drivers ODBC devem apresentar pelo menos a conformidade da interface de nível de núcleo. Como os recursos no nível de núcleo são aqueles exigidos pela maioria dos aplicativos interoperáveis genéricos, o driver pode trabalhar com tais aplicativos. Os recursos no nível de núcleo também correspondem aos recursos definidos na especificação CLI ISO e aos recursos não-opcional definidos na especificação CLI do grupo aberto. Um driver ODBC compatível com a interface de nível de núcleo permite que o aplicativo faça todos os seguintes procedimentos:  
  
-   Aloque e libere todos os tipos de identificadores chamando **SQLAllocHandle** e **SQLFreeHandle**.  
  
-   Use todas as formas da função **SQLFreeStmt** .  
  
-   Associe as colunas do conjunto de resultados, chamando **SQLBindCol**.  
  
-   Manipule parâmetros dinâmicos, incluindo matrizes de parâmetros, somente na direção de entrada, chamando **SQLBindParameter** e **SQLNumParams**. (Os parâmetros na direção de saída são o recurso 203 na [conformidade da interface de nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Especifique um deslocamento de ligação.  
  
-   Use a caixa de diálogo dados em execução, envolvendo chamadas para **SQLParamData** e **SQLPutData**.  
  
-   Gerencie cursores e nomes de cursor, chamando **SQLCloseCursor**, **SQLGetCursorName**e **SQLSetCursorName**.  
  
-   Obter acesso à descrição (metadados) dos conjuntos de resultados, chamando **SQLColAttribute**, **SQLDescribeCol**, **SQLNumResultCols**e **SQLRowCount**. (O uso dessas funções na coluna número 0 para recuperar os metadados do indicador é o recurso 204 na [conformidade da interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Consulte o dicionário de dados, chamando as funções de catálogo **SQLColumns**, **SQLGetTypeInfo**, **SQLStatistics**e **SQLTables**.  
  
     O driver não é necessário para dar suporte a nomes com diversas tabelas e exibições de banco de dados. (Para obter mais informações, consulte o recurso 101 em conformidade com a [interface de nível 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md) e o recurso 201 em conformidade com a [interface de nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).) No entanto, determinados recursos da especificação SQL-92, como a qualificação de coluna e os nomes de índices, são sintaticamente comparáveis à nomenclatura de várias partes. A lista atual de recursos ODBC não se destina a apresentar novas opções nesses aspectos do SQL-92.  
  
-   Gerencie fontes de dados e conexões chamando **SQLConnect**, **SQLDataSources**, **SQLDisconnect**e **SQLDriverConnect**. Obtenha informações sobre drivers, não importa em que nível ODBC eles oferecem suporte, chamando **SQLDrivers**.  
  
-   Preparar e executar instruções SQL, chamando **SQLExecDirect**, **SQLExecute**e **SQLPrepare**.  
  
-   Busque uma linha de um conjunto de resultados ou várias linhas, somente na direção de encaminhamento, chamando **SQLFetch** ou chamando **SQLFetchScroll** com o argumento *FetchOrientation* definido como SQL_FETCH_NEXT.  
  
-   Obtenha uma coluna desassociada em partes, chamando **SQLGetData**.  
  
-   Obtenha os valores atuais de todos os atributos, chamando **SQLGetConnectAttr**, **SQLGetEnvAttr**e **SQLGetStmtAttr**, e defina todos os atributos para seus valores padrão e defina determinados atributos como valores não padrão chamando **SQLSetConnectAttr**, **SQLSetEnvAttr**e **SQLSetStmtAttr**.  
  
-   Manipule determinados campos de descritores chamando **SQLCopyDesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**e **SQLSetDescRec**.  
  
-   Obtenha informações de diagnóstico chamando **SQLGetDiagField** e **SQLGetDiagRec**.  
  
-   Detectar recursos de driver, chamando **SQLGetFunctions** e **SQLGetInfo**. Além disso, detecte o resultado de qualquer substituição de texto feita em uma instrução SQL antes que ela seja enviada para a fonte de dados, chamando **SQLNativeSql**.  
  
-   Use a sintaxe de **SQLEndTran** para confirmar uma transação. Um driver de nível básico não precisa dar suporte a transações verdadeiras; Portanto, o aplicativo não pode especificar SQL_ROLLBACK nem SQL_AUTOCOMMIT_OFF para o atributo de conexão SQL_ATTR_AUTOCOMMIT. (Para obter mais informações, consulte o recurso 109 em conformidade com a [interface de nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Chame **SQLCancel** para cancelar a caixa de diálogo de dados em execução e, em ambientes multithread, para cancelar uma função ODBC em execução em outro thread. A conformidade da interface de nível básico não exige suporte para a execução assíncrona de funções, nem o uso de **SQLCancel** para cancelar uma função ODBC executada de forma assíncrona. Nem a plataforma nem o driver ODBC precisam ser multithread para que o driver realize atividades independentes ao mesmo tempo. No entanto, em ambientes multithread, o driver ODBC deve ser thread-safe. A serialização de solicitações do aplicativo é uma maneira compatível de implementar essa especificação, embora possa criar sérios problemas de desempenho.  
  
-   Obtenha a SQL_BEST_ROWID coluna de identificação de linha de tabelas, chamando **SQLSpecialColumns**. (O suporte para SQL_ROWVER é o recurso 208 na [conformidade da interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
    > [!IMPORTANT]  
    >  Os drivers ODBC devem implementar as funções no nível de conformidade da interface principal.
