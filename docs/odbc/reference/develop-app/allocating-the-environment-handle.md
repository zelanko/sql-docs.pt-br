---
description: Alocar o identificador de ambiente
title: Alocando o identificador de ambiente | Microsoft Docs
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
ms.openlocfilehash: 390d7f4248d43e6fc6cb7910be5f42cb286f37e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429448"
---
# <a name="allocating-the-environment-handle"></a>Alocar o identificador de ambiente
A primeira tarefa para qualquer aplicativo ODBC é carregar o Gerenciador de driver; como isso é feito é dependente do sistema operacional. Por exemplo, em um computador que executa o Microsoft® Windows NT® Server/Windows 2000 Server, Windows NT Workstation/Windows 2000 Professional ou Microsoft Windows® 95/98, o aplicativo se vincula à biblioteca do Driver Manager ou chama **LoadLibrary** para carregar a DLL do Gerenciador de driver.  
  
 A próxima tarefa, que deve ser feita antes que um aplicativo possa chamar qualquer outra função ODBC, é inicializar o ambiente ODBC e alocar um identificador de ambiente, da seguinte maneira:  
  
1.  O aplicativo declara uma variável do tipo SQLHENV. Em seguida, ele chama **SQLAllocHandle** e passa o endereço dessa variável e a opção SQL_HANDLE_ENV. Por exemplo:   
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  O Gerenciador de driver aloca uma estrutura na qual armazenar informações sobre o ambiente e retorna o identificador de ambiente na variável.  
  
 O Gerenciador de driver não chama **SQLAllocHandle** no driver no momento porque ele não sabe qual driver deve ser chamado. Ele atrasa a chamada de **SQLAllocHandle** no driver até que o aplicativo chame uma função para se conectar a uma fonte de dados. Para obter mais informações, consulte [função do Gerenciador de driver no processo de conexão](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), mais adiante nesta seção.  
  
 Quando o aplicativo termina de usar o ODBC, ele libera o identificador de ambiente com **SQLFreeHandle**. Depois de liberar o ambiente, é um erro de programação de aplicativo usar o identificador do ambiente em uma chamada para uma função ODBC; Isso tem conseqüências indefinidas, mas provavelmente fatais.  
  
 Quando **SQLFreeHandle** é chamado, o driver libera a estrutura usada para armazenar informações sobre o ambiente. Observe que **SQLFreeHandle** não pode ser chamado para um identificador de ambiente até que todos os identificadores de conexão nesse identificador de ambiente tenham sido liberados.  
  
 Para obter mais informações sobre o identificador de ambiente, consulte [identificadores de ambiente](../../../odbc/reference/develop-app/environment-handles.md).
