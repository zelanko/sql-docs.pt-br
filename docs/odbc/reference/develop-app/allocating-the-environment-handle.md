---
title: Alocar o identificador de ambiente | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6ac926c39f1390431b35b49b27e7302fe789ca4a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="allocating-the-environment-handle"></a>Alocar o identificador de ambiente
A primeira tarefa para qualquer aplicativo ODBC é carregar o Gerenciador de Driver. como isso é feito depende do sistema operacional. Por exemplo, em um computador executando o Microsoft® Windows NT® Server/Windows 2000 Server, Windows NT Workstation/Windows 2000 Professional ou Microsoft Windows® 95/98, o aplicativo ou links para a biblioteca de Gerenciador de Driver ou chamadas  **LoadLibrary** ao carregar a DLL do Gerenciador de Driver.  
  
 A próxima tarefa, que deve ser feita antes de um aplicativo pode chamar qualquer outra função ODBC, é inicializar o ambiente de ODBC e alocar um identificador de ambiente, da seguinte maneira:  
  
1.  O aplicativo declara uma variável do tipo SQLHENV. Depois, ele chama **SQLAllocHandle** e passa o endereço dessa variável e a opção SQL_HANDLE_ENV. Por exemplo:  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  O Gerenciador de Driver aloca uma estrutura para armazenar informações sobre o ambiente e retorna o identificador de ambiente na variável.  
  
 O Gerenciador de Driver não chama **SQLAllocHandle** no driver neste momento porque ele não sabe qual driver chamar. Atrasar chamada **SQLAllocHandle** no driver até que o aplicativo chama uma função para se conectar a uma fonte de dados. Para obter mais informações, consulte [do Gerenciador de Driver de função no processo de Conexão](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), mais adiante nesta seção.  
  
 Quando o aplicativo terminar de usar o ODBC, ele libera o identificador de ambiente com **SQLFreeHandle**. Depois de liberar o ambiente, é um erro de programação de aplicativo para usar o identificador do ambiente em uma chamada para uma função ODBC; Esse procedimento tem consequências indefinidas, mas provavelmente fatais.  
  
 Quando **SQLFreeHandle** é chamado, as versões de driver a estrutura usada para armazenar informações sobre o ambiente. Observe que **SQLFreeHandle** não pode ser chamado para um identificador de ambiente até depois que todos os identificadores de conexão esse identificador de ambiente foram liberados.  
  
 Para obter mais informações sobre o identificador de ambiente, consulte [trata do ambiente](../../../odbc/reference/develop-app/environment-handles.md).
