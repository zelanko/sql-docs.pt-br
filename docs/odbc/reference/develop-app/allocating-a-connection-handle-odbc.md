---
title: "Alocando um identificador de Conexão ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 678ba0fa4e256402e9fc25e2e4e60ba4877c6c44
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="allocating-a-connection-handle-odbc"></a>Alocando um identificador de Conexão ODBC
Antes do aplicativo pode se conectar a uma fonte de dados ou driver, ele deve alocar um identificador de conexão, da seguinte maneira:  
  
1.  O aplicativo declara uma variável do tipo SQLHDBC. Depois, ele chama **SQLAllocHandle** e passa o endereço dessa variável, o identificador do ambiente no qual a alocar a conexão e a opção SQL_HANDLE_DBC. Por exemplo:  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  O Gerenciador de Driver aloca uma estrutura para armazenar informações sobre a instrução e retorna o identificador de conexão na variável.  
  
 O Gerenciador de Driver não chama **SQLAllocHandle** no driver neste momento porque ele não sabe qual driver chamar. Atrasar chamada **SQLAllocHandle** no driver até que o aplicativo chama uma função para se conectar a uma fonte de dados. Para obter mais informações, consulte [do Gerenciador de Driver de função no processo de Conexão](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), mais adiante nesta seção.  
  
 É importante observar que alocar um identificador de conexão não é igual a carregar um driver. O driver não será carregado até que uma função de conexão é chamada. Assim, depois de alocar um identificador de conexão e antes da conexão com o driver ou fonte de dados, as funções apenas o aplicativo pode chamar com o identificador de conexão são **SQLSetConnectAttr**, **SQLGetConnectAttr**, ou **SQLGetInfo** com a opção SQL_ODBC_VER. Chamar outras funções com o identificador de conexão, como **SQLEndTran**, retorna um SQLSTATE 08003 (Conexão não aberta). Para obter detalhes completos, consulte [tabelas de transição de estado do apêndice b: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obter mais informações sobre identificadores de conexão, consulte [identificadores de Conexão](../../../odbc/reference/develop-app/connection-handles.md).

