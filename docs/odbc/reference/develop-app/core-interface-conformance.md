---
title: Conformidade de Interface de núcleo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c45fdfe2b01ddfd34e7db391b799b95ce696da8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913981"
---
# <a name="core-interface-conformance"></a>Conformidade de Interface de núcleo
Todos os drivers ODBC devem exibir pelo menos nível de núcleo conformidade de interface. Como os recursos no nível de núcleo são aqueles requeridos por aplicativos interoperáveis mais genéricos, o driver pode trabalhar com esses aplicativos. Os recursos no nível de núcleo também correspondem aos recursos definidos na especificação ISO CLI e para os recursos definidos na especificação Open CLI de grupo. Um driver ODBC do nível de núcleo interface – compatível permite que o aplicativo faça o seguinte:  
  
-   Alocar e liberar todos os tipos de identificadores, chamando **SQLAllocHandle** e **SQLFreeHandle**.  
  
-   Usar todas as formas do **SQLFreeStmt** função.  
  
-   Associar colunas do conjunto de resultados, chamando **SQLBindCol**.  
  
-   Lidar com os parâmetros dinâmicos, inclusive matrizes de parâmetros, a direção de entrada apenas, chamando **SQLBindParameter** e **SQLNumParams**. (Parâmetros na direção de saída são recursos 203 em [nível 2 Interface conformidade](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Especifique um deslocamento de ligação.  
  
-   Use a caixa de diálogo de dados em execução que envolvem chamadas para **SQLParamData** e **SQLPutData**.  
  
-   Gerenciar nomes de cursor e cursores chamando **SQLCloseCursor**, **SQLGetCursorName**, e **SQLSetCursorName**.  
  
-   Acessar a descrição (metadados) de conjuntos de resultados chamando **SQLColAttribute**, **SQLDescribeCol**, **SQLNumResultCols**, e **SQLRowCount** . (Uso dessas funções na coluna número 0 para recuperar metadados de indicador é recurso 204 em [nível 2 Interface conformidade](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   O dicionário de dados de consulta ao chamar as funções de catálogo **SQLColumns**, **SQLGetTypeInfo**, **SQLStatistics**, e **SQLTables**.  
  
     O driver não é necessário para dar suporte a nomes de várias partes de tabelas de banco de dados e exibições. (Para obter mais informações, consulte o recurso 101 no [nível 1 Interface conformidade](../../../odbc/reference/develop-app/level-1-interface-conformance.md) e recurso 201 no [nível 2 Interface conformidade](../../../odbc/reference/develop-app/level-2-interface-conformance.md).) No entanto, alguns recursos da especificação SQL-92, como nomes de índices e qualificação de coluna são sintaticamente comparáveis a nomenclatura de várias partes. A lista atual de recursos ODBC não se destina para introduzir novas opções para os seguintes aspectos de SQL-92.  
  
-   Gerenciar fontes de dados e conexões, chamando **SQLConnect**, **SQLDataSources**, **SQLDisconnect**, e **SQLDriverConnect**. Obter informações sobre drivers, independentemente de qual ODBC nível dão suporte, chamando **SQLDrivers**.  
  
-   Preparar e executar instruções SQL, chamando **SQLExecDirect**, **SQLExecute**, e **SQLPrepare**.  
  
-   Buscar uma linha de um conjunto de resultados ou várias linhas, no sentido de encaminhamento, chamando **SQLFetch** ou chamando **SQLFetchScroll** com o *FetchOrientation* argumento Defina como SQL_FETCH_NEXT.  
  
-   Obter uma coluna não associada em partes, chamando **SQLGetData**.  
  
-   Obter os valores atuais de todos os atributos, chamando **SQLGetConnectAttr**, **SQLGetEnvAttr**, e **SQLGetStmtAttr**e defina todos os atributos para os valores padrão e Definir determinados atributos para valores não padrão chamando **SQLSetConnectAttr**, **SQLSetEnvAttr**, e **SQLSetStmtAttr**.  
  
-   Manipular determinados campos de descritores, chamando **SQLCopyDesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**, e **SQLSetDescRec**.  
  
-   Obter informações de diagnóstico, chamando **SQLGetDiagField** e **SQLGetDiagRec**.  
  
-   Detectar recursos de driver, chamando **SQLGetFunctions** e **SQLGetInfo**. Além disso, detectar o resultado de qualquer substituições de texto feitas para uma instrução SQL antes de serem enviado para a fonte de dados, chamando **SQLNativeSql**.  
  
-   Use a sintaxe de **SQLEndTran** para confirmar uma transação. Um driver de nível de núcleo não precisa oferecer suporte a transações true; Portanto, o aplicativo não é possível especificar SQL_ROLLBACK nem SQL_AUTOCOMMIT_OFF para o atributo de conexão SQL_ATTR_AUTOCOMMIT. (Para obter mais informações, consulte o recurso 109 no [nível 2 Interface conformidade](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Chamar **SQLCancel** para cancelar a caixa de diálogo de dados em execução e, em ambientes de vários threads, para cancelar uma função ODBC executando em outro thread. Conformidade de interface de nível de núcleo não exige suporte para execução assíncrona de funções, nem o uso de **SQLCancel** para cancelar uma função ODBC em execução assíncrona. A plataforma, nem o driver ODBC precisa ser multithread para o driver realizar atividades independentes ao mesmo tempo. No entanto, em ambientes de vários threads, o driver ODBC deve ser thread-safe. Serialização de solicitações do aplicativo é uma maneira de compatível para implementar essa especificação, mesmo que ele pode criar sérios problemas de desempenho.  
  
-   Obter a coluna de identificação de linha SQL_BEST_ROWID de tabelas, chamando **SQLSpecialColumns**. (Suporte para SQL_ROWVER é recurso 208 em [nível 2 Interface conformidade](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
    > [!IMPORTANT]  
    >  Drivers ODBC deve implementar as funções em nível de conformidade da interface principal.
