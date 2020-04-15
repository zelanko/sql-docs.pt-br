---
title: Alocando uma alça de conexão ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12e9f65ee81612e269c1f86ebabd049588443cb8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288516"
---
# <a name="allocating-a-connection-handle-odbc"></a>Alocar um identificador de conexão ODBC
Antes que o aplicativo possa se conectar a uma fonte de dados ou driver, ele deve alocar uma alça de conexão, da seguinte forma:  
  
1.  O aplicativo declara uma variável do tipo SQLHDBC. Em seguida, ele chama **SQLAllocHandle** e passa o endereço desta variável, a alça do ambiente em que alocar a conexão e a opção SQL_HANDLE_DBC. Por exemplo:  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  O Driver Manager aloca uma estrutura na qual armazenar informações sobre a declaração e retorna a alça de conexão na variável.  
  
 O Driver Manager não chama **SQLAllocHandle** no driver neste momento porque não sabe qual motorista chamar. Ele atrasa a chamada **SQLAllocHandle** no driver até que o aplicativo chame uma função para se conectar a uma fonte de dados. Para obter mais informações, consulte [a função do driver manager no processo de conexão,](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)mais tarde nesta seção.  
  
 É importante notar que alocar uma alça de conexão não é o mesmo que carregar um driver. O driver não é carregado até que uma função de conexão seja chamada. Assim, depois de alocar uma alça de conexão e antes de se conectar ao driver ou à fonte de dados, as únicas funções que o aplicativo pode chamar com a alça de conexão são **SQLSetConnectAttr,** **SQLGetConnectAttr**ou **SQLGetInfo** com a opção SQL_ODBC_VER. Chamando outras funções com o cabo de conexão, como **SQLEndTran**, retorna SQLSTATE 08003 (Conexão não aberta). Para obter detalhes completos, consulte [apêndice B: Tabelas de transição do estado oDBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obter mais informações sobre as alças de conexão, consulte [Alças de conexão](../../../odbc/reference/develop-app/connection-handles.md).
