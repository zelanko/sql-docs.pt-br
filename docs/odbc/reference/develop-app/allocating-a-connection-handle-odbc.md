---
title: Alocando um identificador de conexão ODBC | Microsoft Docs
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
ms.openlocfilehash: 3bd3a44fe4f0466dfcf11a72fa0377564c1cf02f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077210"
---
# <a name="allocating-a-connection-handle-odbc"></a>Alocar um identificador de conexão ODBC
Antes que o aplicativo possa se conectar a uma fonte de dados ou driver, ele deve alocar um identificador de conexão, da seguinte maneira:  
  
1.  O aplicativo declara uma variável do tipo SQLHDBC. Em seguida, ele chama **SQLAllocHandle** e passa o endereço dessa variável, o identificador do ambiente no qual alocar a conexão e a opção SQL_HANDLE_DBC. Por exemplo:  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  O Gerenciador de driver aloca uma estrutura na qual armazenar informações sobre a instrução e retorna o identificador de conexão na variável.  
  
 O Gerenciador de driver não chama **SQLAllocHandle** no driver no momento porque ele não sabe qual driver deve ser chamado. Ele atrasa a chamada de **SQLAllocHandle** no driver até que o aplicativo chame uma função para se conectar a uma fonte de dados. Para obter mais informações, consulte [função do Gerenciador de driver no processo de conexão](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), mais adiante nesta seção.  
  
 É importante observar que alocar um identificador de conexão não é o mesmo que carregar um driver. O driver não é carregado até que uma função de conexão seja chamada. Portanto, depois de alocar um identificador de conexão e antes de se conectar ao driver ou à fonte de dados, as funções únicas que o aplicativo pode chamar com o identificador de conexão são **SQLSetConnectAttr**, **SQLGetConnectAttr**ou **SQLGetInfo** com a opção SQL_ODBC_VER. Chamar outras funções com o identificador de conexão, como **SQLEndTran**, retorna SQLSTATE 08003 (conexão não aberta). Para obter detalhes completos, consulte o [Apêndice B: tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obter mais informações sobre identificadores de conexão, consulte [identificadores de conexão](../../../odbc/reference/develop-app/connection-handles.md).
