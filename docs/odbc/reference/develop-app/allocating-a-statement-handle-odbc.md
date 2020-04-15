---
title: Alocando uma Alça de Declaração ODBC | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288426"
---
# <a name="allocating-a-statement-handle-odbc"></a>Alocar um identificador de instrução ODBC
Antes que o aplicativo possa executar uma declaração, ele deve alocar uma alça de declaração da seguinte forma:  
  
1.  O aplicativo declara uma variável do tipo HSTMT. Em seguida, ele chama **SQLAllocHandle** e passa o endereço desta variável, a alça da conexão em que alocar a declaração e a opção SQL_HANDLE_STMT. Por exemplo:  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  O Driver Manager aloca uma estrutura na qual armazenar informações sobre a declaração e chama **SQLAllocHandle** no driver com a opção SQL_HANDLE_STMT.  
  
3.  O motorista aloca sua própria estrutura para armazenar informações sobre a declaração e devolve a alça da declaração do motorista ao Driver Manager.  
  
4.  O Gerenciador de driver retorna a alça de declaração do Driver Manager para o aplicativo na variável de aplicativo.  
  
 O identificador de declaração identifica qual declaração usar ao ligar para funções ODBC. Para obter mais informações sobre as alças de declaração, consulte ['Alças de declaração'](../../../odbc/reference/develop-app/statement-handles.md)
