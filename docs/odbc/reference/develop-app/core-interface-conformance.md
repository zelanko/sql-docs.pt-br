---
title: Conformidade de Interface Central | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302128"
---
# <a name="core-interface-conformance"></a>Conformidade de interface de núcleo
Todos os drivers ODBC devem exibir pelo menos conformidade de interface de nível core. Como os recursos no nível Core são os exigidos pela maioria dos aplicativos interoperáveis genéricos, o motorista pode trabalhar com tais aplicativos. Os recursos no nível Core também correspondem aos recursos definidos na especificação ISO CLI e aos recursos não opcionais definidos na especificação CLI do Grupo Aberto. Um driver ODBC de interface de nível de núcleo permite que o aplicativo faça tudo o que é:  
  
-   Aloque e liberte todos os tipos de alças, ligando para **SQLAllocHandle** e **SQLFreeHandle**.  
  
-   Use todas as formas da função **SQLFreeStmt.**  
  
-   Vincular colunas de conjunto de resultados, chamando **SQLBindCol**.  
  
-   Lidar com parâmetros dinâmicos, incluindo matrizes de parâmetros, apenas na direção de entrada, chamando **SQLBindParams** e **SQLNumParams**. (Os parâmetros na direção da saída são o recurso 203 na [Conformidade de Interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Especifique um deslocamento de vinculação.  
  
-   Use a caixa de diálogo data-at-execution, envolvendo chamadas para **SQLParamData** e **SQLPutData**.  
  
-   Gerencie os nomes de cursores e cursores, chamando **SQLCloseCursor,** **SQLGetCursorName**e **SQLSetCursorName**.  
  
-   Obtenha acesso à descrição (metadados) dos conjuntos de resultados, ligando para **SQLColAttribute,** **SQLDescribeCol,** **SQLNumResultCols**e **SQLRowCount**. (O uso dessas funções na coluna número 0 para recuperar metadados de marcadores é o recurso 204 na [Conformidade de Interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Consulta o dicionário de dados, chamando as funções de catálogo **sqlColumns,** **SQLGetTypeInfo,** **SQLStatistics**e **SQLTables**.  
  
     O driver não é obrigado a suportar nomes de várias partes de tabelas e visualizações de banco de dados. (Para obter mais informações, consulte o recurso 101 no [Nível 1 de Conformidade de Interface](../../../odbc/reference/develop-app/level-1-interface-conformance.md) e apresente 201 no Nível 2 de Conformidade de [Interface](../../../odbc/reference/develop-app/level-2-interface-conformance.md).) No entanto, certas características da especificação SQL-92, como qualificação de colunas e nomes de índices, são sintáticamente comparáveis à nomenclatura multiparte. A presente lista de recursos do ODBC não se destina a introduzir novas opções nesses aspectos do SQL-92.  
  
-   Gerencie fontes e conexões de dados, ligando para **SQLConnect,** **SQLDataSources,** **SQLDisconnect**e **SQLDriverConnect**. Obtenha informações sobre drivers, não importa qual nível ODBC eles suportam, ligando para **SQLDrivers**.  
  
-   Preparar e executar instruções SQL, chamando **SQLExecDirect,** **SQLExecute**e **SQLPrepare**.  
  
-   Busque uma linha de um conjunto de resultados ou várias linhas, apenas na direção para a frente, ligando para **SQLFetch** ou ligando para **SQLFetchScroll** com o argumento *FetchOrientation* definido para SQL_FETCH_NEXT.  
  
-   Obtenha uma coluna desvinculada em partes, ligando para **SQLGetData**.  
  
-   Obtenha valores atuais de todos os atributos, chamando **SQLGetConnectAttr,** **SQLGetEnvAttr**e **SQLGetStmtAttr**, e defina todos os atributos para seus valores padrão e defina certos atributos para valores não padrão, chamando **SQLSetConnectAttr,** **SQLSetEnvAttr**e **SQLSetStmtAttr**.  
  
-   Manipular certos campos de descritores, ligando para **SQLCopyDesc,** **SQLGetDescField,** **SQLGetDescRec,** **SQLSetDescField**e **SQLSetDescRec**.  
  
-   Obtenha informações de diagnóstico, ligando para **SQLGetDiagField** e **SQLGetDiagRec**.  
  
-   Detecte os recursos do driver, chamando **SQLGetFunctions** e **SQLGetInfo**. Além disso, detecte o resultado de quaisquer substituições de texto feitas em uma declaração SQL antes de ser enviada à fonte de dados, ligando para **SQLNativeSql**.  
  
-   Use a sintaxe do **SQLEndTran** para cometer uma transação. Um driver de nível core não precisa suportar transações verdadeiras; portanto, o aplicativo não pode especificar SQL_ROLLBACK nem SQL_AUTOCOMMIT_OFF para o atributo de conexão SQL_ATTR_AUTOCOMMIT. (Para obter mais informações, consulte o recurso 109 na [Conformidade de Interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Ligue para o **SQLCancel** para cancelar a caixa de diálogo data-at-execution e, em ambientes multithread, cancelar uma função ODBC em execução em outro segmento. A conformidade de interface de nível de núcleo não exige suporte para execução assíncrona de funções, nem o uso de **SQLCancel** para cancelar uma função ODBC executando de forma assíncrona. Nem a plataforma nem o driver ODBC precisam ser multithread para que o motorista realize atividades independentes ao mesmo tempo. No entanto, em ambientes multithread, o driver ODBC deve ser seguro para rosca. A serialização das solicitações do aplicativo é uma forma de implementar essa especificação, embora possa criar sérios problemas de desempenho.  
  
-   Obtenha a SQL_BEST_ROWID coluna de identificação de linhas de tabelas, ligando para **SQLSpecialColumns**. (O suporte para SQL_ROWVER é o recurso 208 na [Conformidade de Interface Nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
    > [!IMPORTANT]  
    >  Os drivers ODBC devem implementar as funções no nível de conformidade da interface Core.
