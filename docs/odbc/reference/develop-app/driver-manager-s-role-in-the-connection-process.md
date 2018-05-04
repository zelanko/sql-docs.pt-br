---
title: O Gerenciador de driver&#39;s função no processo de Conexão | Microsoft Docs
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
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85839606036b56f058f6347b57d45ca296e23b96
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>O Gerenciador de driver&#39;s função no processo de Conexão
Lembre-se de que aplicativos não chamar funções de driver diretamente. Em vez disso, eles chamam funções do Gerenciador de Driver com o mesmo nome e o Gerenciador de Driver chama as funções de driver. Geralmente, isso acontece quase imediatamente. Por exemplo, o aplicativo chama **SQLExecute** no Gerenciador de Driver e depois de algumas verificações de erro, o Gerenciador de Driver chamará **SQLExecute** no driver.  
  
 O processo de conexão é diferente. Quando o aplicativo chama **SQLAllocHandle** com as opções SQL_HANDLE_ENV e SQL_HANDLE_DBC, a função aloca identificadores somente no Gerenciador de Driver. O Gerenciador de Driver não chama essa função no driver porque ele não sabe qual driver chamar. Da mesma forma, se o aplicativo passa o identificador de uma conexão desconectado para **SQLSetConnectAttr** ou **SQLGetConnectAttr**, somente o Gerenciador de Driver executa a função. Ele armazena ou obtém o valor do atributo de sua conexão manipular e retorna o SQLSTATE 08003 (Conexão não aberta) ao obter um valor para um atributo que não foi definido e para quais ODBC não define um valor padrão.  
  
 Quando o aplicativo chama **SQLConnect**, **SQLDriverConnect**, ou **SQLBrowseConnect**, o Gerenciador de Driver primeiro determina qual driver usar. Em seguida, ele verifica para determinar se um driver é carregado no momento em que a conexão:  
  
-   Se nenhum driver foi carregado na conexão, o Gerenciador de Driver verifica se o driver especificado é carregado em outra conexão no mesmo ambiente. Se não, o Gerenciador de Driver carrega o driver na conexão e chama **SQLAllocHandle** no driver com a opção SQL_HANDLE_ENV.  
  
     Em seguida, chama o Gerenciador de Driver **SQLAllocHandle** no driver com a opção SQL_HANDLE_DBC, ou não foi carregado apenas. Se o aplicativo definir quaisquer atributos de conexão, o Gerenciador de Driver chamará **SQLSetConnectAttr** no driver; se ocorrer um erro, função de conexão do Gerenciador de Driver retornará SQLSTATE IM006 (do Driver  **SQLSetConnectAttr** falha). Por fim, o Gerenciador de Driver chama a função de conexão no driver.  
  
-   Se o driver especificado é carregado na conexão, o Gerenciador de Driver chama a função de conexão no driver. Nesse caso, o driver deve garantir que todos os atributos de conexão a conexão mantenham suas configurações atuais.  
  
-   Se um driver diferente é carregado na conexão, o Gerenciador de Driver chamará **SQLFreeHandle** no driver para liberar a conexão. Se não houver nenhuma outra conexão que usam o driver, o Gerenciador de Driver chama **SQLFreeHandle** no driver para liberar o ambiente e descarrega o driver. O Gerenciador de Driver, em seguida, executa as mesmas operações como quando um driver não está carregado na conexão.  
  
 O Gerenciador de Driver bloqueará o identificador de ambiente (*henv*) antes de chamar um driver **SQLAllocHandle** e **SQLFreeHandle** quando *HandleType* é definido como **SQL_HANDLE_DBC**.  
  
 Quando o aplicativo chama **SQLDisconnect**, as chamadas de Gerenciador de Driver **SQLDisconnect** no driver. No entanto, ele deixa o driver carregado no caso do aplicativo se reconecta ao driver. Quando o aplicativo chama **SQLFreeHandle** com a opção SQL_HANDLE_DBC, chama o Gerenciador de Driver **SQLFreeHandle** no driver. Se o driver não for usado por qualquer outra conexão, em seguida, chama o Gerenciador de Driver **SQLFreeHandle** no driver com o SQL_HANDLE_ENV opção e descarrega o driver.
