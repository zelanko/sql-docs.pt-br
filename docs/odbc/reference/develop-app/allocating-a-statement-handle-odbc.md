---
title: Alocar um identificador de instrução ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: faef5961418634f36f69a0f940e59c3e3b2b16cd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="allocating-a-statement-handle-odbc"></a>Alocar um identificador de instrução ODBC
Antes do aplicativo pode executar uma instrução, ele deve alocar um identificador de instrução da seguinte maneira:  
  
1.  O aplicativo declara uma variável do tipo HSTMT. Depois, ele chama **SQLAllocHandle** e passa o endereço dessa variável, o identificador de conexão de alocação a instrução e a opção de SQL_HANDLE_STMT. Por exemplo:  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  O Gerenciador de Driver aloca uma estrutura para armazenar informações sobre a instrução e chamadas **SQLAllocHandle** no driver com a opção de SQL_HANDLE_STMT.  
  
3.  O driver aloca sua própria estrutura na qual armazenar informações sobre a instrução e retorna o identificador de instrução de driver para o Gerenciador de Driver.  
  
4.  O Gerenciador de Driver retorna o identificador de instrução do Gerenciador de Driver para o aplicativo na variável de aplicativo.  
  
 O identificador de instrução identifica qual instrução a ser usado ao chamar funções ODBC. Para obter mais informações sobre identificadores de instrução, consulte [identificadores de instrução](../../../odbc/reference/develop-app/statement-handles.md).
