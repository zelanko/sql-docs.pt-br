---
title: Conformidade de Interface de núcleo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02e8aabf808ebf11f2e241fc7d330f794dbb0112
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002112"
---
# <a name="core-interface-conformance"></a>Conformidade de interface de núcleo
Todos os drivers ODBC devem apresentar pelo menos nível de núcleo conformidade de interface. Como os recursos no nível de núcleo são aquelas necessárias para aplicativos interoperáveis mais genéricos, o driver pode trabalhar com esses aplicativos. Os recursos no nível de núcleo também correspondem aos recursos definidos na especificação de CLI ISO e para os recursos definidos na especificação de CLI de grupo aberto. Um driver ODBC do nível de núcleo compatível com o interface permite que o aplicativo faça o seguinte:  
  
-   Alocar e liberar todos os tipos de identificadores, chamando **SQLAllocHandle** e **SQLFreeHandle**.  
  
-   Usar todas as formas dos **SQLFreeStmt** função.  
  
-   Associar colunas do conjunto de resultados, chamando **SQLBindCol**.  
  
-   Lidar com parâmetros dinâmicos, incluindo matrizes de parâmetros de entrada somente na direção, chamando **SQLBindParameter** e **SQLNumParams**. (Parâmetros na direção de saída são recursos 203 na [conformidade de Interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Especifique um deslocamento de ligação.  
  
-   Use a caixa de diálogo de dados em execução, que envolvem chamadas para **SQLParamData** e **SQLPutData**.  
  
-   Gerenciar cursores e nomes de cursor chamando **SQLCloseCursor**, **SQLGetCursorName**, e **SQLSetCursorName**.  
  
-   Obter acesso a descrição (metadados) de conjuntos de resultados, chamando **SQLColAttribute**, **SQLDescribeCol**, **SQLNumResultCols**, e **SQLRowCount** . (Uso dessas funções na coluna número 0 para recuperar metadados de indicador é recurso 204 no [conformidade de Interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Consultar o dicionário de dados, chamando as funções de catálogo **SQLColumns**, **SQLGetTypeInfo**, **SQLStatistics**, e **SQLTables**.  
  
     O driver não é necessário para dar suporte a nomes de várias partes de tabelas de banco de dados e exibições. (Para obter mais informações, consulte o recurso de 101 na [conformidade de Interface nível 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md) e o recurso 201 na [conformidade de Interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).) No entanto, alguns recursos da especificação SQL-92, como nomes de índices e qualificação de coluna são sintaticamente comparáveis à nomenclatura de várias partes. A lista de presente de recursos de ODBC não se destina a apresentar novas opções para esses aspectos do SQL-92.  
  
-   Gerenciar fontes de dados e conexões, chamando **SQLConnect**, **SQLDataSources**, **SQLDisconnect**, e **SQLDriverConnect**. Obter informações sobre drivers, independentemente de qual ODBC nível eles suportam, chamando **SQLDrivers**.  
  
-   Preparar e executar instruções SQL, chamando **SQLExecDirect**, **SQLExecute**, e **SQLPrepare**.  
  
-   Buscar uma linha de um conjunto de resultados ou várias linhas, apenas, da direção para frente chamando **SQLFetch** ou chamando **SQLFetchScroll** com o *FetchOrientation* argumento Defina como SQL_FETCH_NEXT.  
  
-   Obter uma coluna não associada em partes, chamando **SQLGetData**.  
  
-   Obter os valores atuais de todos os atributos, chamando **SQLGetConnectAttr**, **SQLGetEnvAttr**, e **SQLGetStmtAttr**e defina todos os atributos para seus valores padrão e definir certos atributos a valores não padrão chamando **SQLSetConnectAttr**, **SQLSetEnvAttr**, e **SQLSetStmtAttr**.  
  
-   Manipular determinados campos de descritores, chamando **SQLCopyDesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**, e **SQLSetDescRec**.  
  
-   Obter informações de diagnóstico, chamando **SQLGetDiagField** e **SQLGetDiagRec**.  
  
-   Detectar recursos de driver, chamando **SQLGetFunctions** e **SQLGetInfo**. Além disso, detectar o resultado de qualquer substituições de texto feitas para uma instrução SQL antes de serem enviado à fonte de dados, chamando **SQLNativeSql**.  
  
-   Use a sintaxe da **SQLEndTran** para confirmar uma transação. Um driver de nível de núcleo não precisa suportar transações true; Portanto, o aplicativo não é possível especificar SQL_ROLLBACK nem SQL_AUTOCOMMIT_OFF para o atributo de conexão SQL_ATTR_AUTOCOMMIT. (Para obter mais informações, consulte o recurso 109 no [conformidade de Interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Chame **SQLCancel** para cancelar a caixa de diálogo de dados em execução e, em ambientes com vários threads, para cancelar uma função ODBC executando em outro thread. Conformidade de interface de nível de núcleo não exige suporte para a execução assíncrona de funções, nem o uso de **SQLCancel** para cancelar uma função ODBC em execução assíncrona. Nem a plataforma nem o driver ODBC precisa ser multithread para o driver realizar atividades independentes ao mesmo tempo. No entanto, em ambientes com vários threads, o driver ODBC deve ser thread-safe. Serialização solicitações do aplicativo é uma maneira de acordo com as conformidades para implementar essa especificação, mesmo que ele pode criar problemas graves de desempenho.  
  
-   Obter a coluna de identificação de linha SQL_BEST_ROWID de tabelas, chamando **SQLSpecialColumns**. (208 de recursos é suporte para SQL_ROWVER [conformidade de Interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
    > [!IMPORTANT]  
    >  Drivers ODBC deve implementar as funções em nível de conformidade de interface de núcleo.
