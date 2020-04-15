---
title: Alocando a Alça do Meio Ambiente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e33b850b2786960a368720deaf89a2203c7dd159
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302999"
---
# <a name="allocating-the-environment-handle"></a>Alocar o identificador de ambiente
A primeira tarefa para qualquer aplicativo ODBC é carregar o Driver Manager; como isso é feito é dependente do sistema operacional. Por exemplo, em um computador que executa o Microsoft® O Servidor do Windows® Server/Windows 2000, o Windows NT Workstation/Windows 2000 Professional ou o Microsoft Windows® 95/98, o aplicativo vincula-se à biblioteca do Gerenciador de driver ou chama **loadLibrary** para carregar o DLL do Driver Manager.  
  
 A próxima tarefa, que deve ser feita antes que um aplicativo possa chamar qualquer outra função ODBC, é inicializar o ambiente ODBC e alocar uma alça de ambiente, da seguinte forma:  
  
1.  O aplicativo declara uma variável do tipo SQLHENV. Em seguida, ele chama **SQLAllocHandle** e passa o endereço desta variável e a opção SQL_HANDLE_ENV. Por exemplo:  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  O Driver Manager aloca uma estrutura na qual armazenar informações sobre o ambiente e devolve a alça do ambiente na variável.  
  
 O Driver Manager não chama **SQLAllocHandle** no driver neste momento porque não sabe qual motorista chamar. Ele atrasa a chamada **SQLAllocHandle** no driver até que o aplicativo chame uma função para se conectar a uma fonte de dados. Para obter mais informações, consulte [a função do driver manager no processo de conexão,](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)mais tarde nesta seção.  
  
 Quando o aplicativo tiver terminado usando o ODBC, ele libera o cabo do ambiente com **sQLFreeHandle**. Depois de liberar o ambiente, é um erro de programação de aplicativos usar a alça do ambiente em uma chamada para uma função ODBC; fazê-lo tem consequências indefinidas, mas provavelmente fatais.  
  
 Quando **o SQLFreeHandle** é chamado, o driver libera a estrutura usada para armazenar informações sobre o ambiente. Observe que **o SQLFreeHandle** não pode ser chamado para uma alça de ambiente até que todas as alças de conexão na alça do ambiente tenham sido liberadas.  
  
 Para obter mais informações sobre o manuseio do ambiente, consulte [Environment Handles](../../../odbc/reference/develop-app/environment-handles.md).
