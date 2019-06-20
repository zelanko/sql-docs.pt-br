---
title: Alocando um identificador de Conexão ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83964bf1e76eef5c7c4ba4121b0c581e8d8a406b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288323"
---
# <a name="allocating-a-connection-handle-odbc"></a>Alocar um identificador de conexão ODBC
Antes do aplicativo pode se conectar a uma fonte de dados ou o driver, ele deve alocar um identificador de conexão, da seguinte maneira:  
  
1.  O aplicativo declara uma variável do tipo SQLHDBC. Em seguida, ele chama **SQLAllocHandle** e passa o endereço dessa variável, o identificador do ambiente no qual alocar a conexão e a opção SQL_HANDLE_DBC. Por exemplo:  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  O Gerenciador de Driver aloca uma estrutura na qual armazenar informações sobre a instrução e retorna o identificador de conexão na variável.  
  
 O Gerenciador de Driver não chama **SQLAllocHandle** no driver isso porque ele não sabe qual driver a ser chamada de tempo. Atrasa a chamada **SQLAllocHandle** no driver até que o aplicativo chama uma função para se conectar a uma fonte de dados. Para obter mais informações, consulte [do Gerenciador de Driver de função no processo de Conexão](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), mais adiante nesta seção.  
  
 É importante observar que alocando um identificador de conexão não é o mesmo que o carregamento de um driver. O driver não será carregado até que uma função de conexão é chamada. Portanto, depois de alocar um identificador de conexão e antes de se conectar ao driver ou fonte de dados, as funções apenas o aplicativo pode chamar com o identificador de conexão são **SQLSetConnectAttr**, **SQLGetConnectAttr**, ou **SQLGetInfo** com a opção SQL_ODBC_VER. Chamar outras funções com o identificador de conexão, como **SQLEndTran**, retorna um SQLSTATE 08003 (Conexão não está aberta). Para obter detalhes completos, consulte [apêndice b: Tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obter mais informações sobre identificadores de conexão, consulte [identificadores de Conexão](../../../odbc/reference/develop-app/connection-handles.md).
