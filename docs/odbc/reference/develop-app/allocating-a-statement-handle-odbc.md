---
title: Alocando um identificador de instrução ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf9a15bc4622b15afa9838327edd90383a812270
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288426"
---
# <a name="allocating-a-statement-handle-odbc"></a>Alocar um identificador de instrução ODBC
Antes que o aplicativo possa executar uma instrução, ele deve alocar um identificador de instrução da seguinte maneira:  
  
1.  O aplicativo declara uma variável do tipo HSTMT. Em seguida, ele chama **SQLAllocHandle** e passa o endereço dessa variável, o identificador da conexão na qual alocar a instrução e a opção SQL_HANDLE_STMT. Por exemplo:  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  O Gerenciador de driver aloca uma estrutura na qual armazenar informações sobre a instrução e chama **SQLAllocHandle** no driver com a opção SQL_HANDLE_STMT.  
  
3.  O driver aloca sua própria estrutura na qual armazenar informações sobre a instrução e retorna o identificador da instrução do driver para o Gerenciador de driver.  
  
4.  O Gerenciador de driver retorna o identificador de instrução do Gerenciador de driver para o aplicativo na variável de aplicativo.  
  
 O identificador de instrução identifica qual instrução usar ao chamar funções ODBC. Para obter mais informações sobre identificadores de instrução, consulte [identificadores de instrução](../../../odbc/reference/develop-app/statement-handles.md).
