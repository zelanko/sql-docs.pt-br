---
title: Função de&#39;s do Gerenciador de driver no processo de conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0227a4063573cb05ecaa9434605ba35f2811bd06
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305797"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>Função de&#39;s do Gerenciador de driver no processo de conexão
Lembre-se de que os aplicativos não chamam funções de driver diretamente. Em vez disso, eles chamam as funções do Gerenciador de driver com o mesmo nome e o Gerenciador de driver chama as funções de driver. Normalmente, isso ocorre quase imediatamente. Por exemplo, o aplicativo chama **SQLExecute** no Gerenciador de driver e, após algumas verificações de erro, o Gerenciador de driver chama **SQLExecute** no driver.  
  
 O processo de conexão é diferente. Quando o aplicativo chama **SQLAllocHandle** com as opções SQL_HANDLE_ENV e SQL_HANDLE_DBC, a função aloca identificadores somente no Gerenciador de driver. O Gerenciador de driver não chama essa função no driver porque não sabe qual driver deve ser chamado. Da mesma forma, se o aplicativo passar o identificador de uma conexão não conectada para **SQLSetConnectAttr** ou **SQLGetConnectAttr**, somente o Gerenciador de driver executará a função. Ele armazena ou Obtém o valor do atributo de seu identificador de conexão e retorna o SQLSTATE 08003 (conexão não aberta) ao obter um valor para um atributo que não foi definido e para o qual o ODBC não define um valor padrão.  
  
 Quando o aplicativo chama **SQLConnect**, **SQLDriverConnect**ou **SQLBrowseConnect**, o Gerenciador de driver primeiro determina qual driver usar. Em seguida, ele verifica para determinar se um driver está carregado atualmente na conexão:  
  
-   Se nenhum driver for carregado na conexão, o Gerenciador de driver verificará se o driver especificado está carregado em outra conexão no mesmo ambiente. Caso contrário, o Gerenciador de driver carregará o driver na conexão e chamará **SQLAllocHandle** no driver com a opção SQL_HANDLE_ENV.  
  
     Em seguida, o Gerenciador de driver chama **SQLAllocHandle** no driver com a opção SQL_HANDLE_DBC, quer ele tenha acabado de ser carregado ou não. Se o aplicativo definir qualquer atributo de conexão, o Gerenciador de driver chamará **SQLSetConnectAttr** no driver; Se ocorrer um erro, a função de conexão do Gerenciador de driver retornará SQLSTATE IM006 (o **SQLSetConnectAttr** do driver falhou). Por fim, o Gerenciador de driver chama a função de conexão no driver.  
  
-   Se o driver especificado for carregado na conexão, o Gerenciador de driver chamará apenas a função de conexão no driver. Nesse caso, o driver deve garantir que todos os atributos de conexão na conexão mantenham suas configurações atuais.  
  
-   Se um driver diferente for carregado na conexão, o Gerenciador de driver chamará **SQLFreeHandle** no driver para liberar a conexão. Se não houver nenhuma outra conexão que use o driver, o Gerenciador de driver chamará **SQLFreeHandle** no driver para liberar o ambiente e descarregará o driver. Em seguida, o Gerenciador de driver executa as mesmas operações que quando um driver não é carregado na conexão.  
  
 O Gerenciador de driver bloqueará o identificador de ambiente (*HENV*) antes de chamar o **SQLAllocHandle** e o **SQLFreeHandle** de um driver quando *HandleType* for definido como **SQL_HANDLE_DBC**.  
  
 Quando o aplicativo chama **SQLDisconnect**, o Gerenciador de driver chama **SQLDisconnect** no driver. No entanto, ele deixa o driver carregado, caso o aplicativo se reconecte ao driver. Quando o aplicativo chama **SQLFreeHandle** com a opção SQL_HANDLE_DBC, o Gerenciador de driver chama **SQLFreeHandle** no driver. Se o driver não for usado por nenhuma outra conexão, o Gerenciador de driver chamará **SQLFreeHandle** no driver com a opção SQL_HANDLE_ENV e descarregará o driver.
