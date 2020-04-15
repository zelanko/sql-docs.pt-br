---
title: Driver Manager&#39;papel no processo de conexão | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305797"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>Driver Manager&#39;papel no processo de conexão
Lembre-se que os aplicativos não chamam diretamente as funções do driver. Em vez disso, eles chamam funções de Driver Manager com o mesmo nome e o Gerenciador de Driver chama as funções do driver. Normalmente, isso acontece quase imediatamente. Por exemplo, o aplicativo chama **SQLExecute** no Gerenciador de driver e após algumas verificações de erro, o Gerenciador de driver chama **SQLExecute** no driver.  
  
 O processo de conexão é diferente. Quando o aplicativo chama **SQLAllocHandle** com as opções de SQL_HANDLE_ENV e SQL_HANDLE_DBC, a função aloca as alças apenas no Gerenciador de Driver. O Driver Manager não chama essa função no motorista porque não sabe qual motorista chamar. Da mesma forma, se o aplicativo passar a alça de uma conexão não conectada ao **SQLSetConnectAttr** ou **ao SQLGetConnectAttr,** apenas o Driver Manager executará a função. Ele armazena ou obtém o valor de atributo de sua alça de conexão e retorna SQLSTATE 08003 (Conexão não aberta) ao obter um valor para um atributo que não foi definido e para o qual o ODBC não define um valor padrão.  
  
 Quando o aplicativo chama **SQLConnect,** **SQLDriverConnect**ou **SQLBrowseConnect,** o Driver Manager determina primeiro qual driver usar. Em seguida, verifica se um driver está carregado atualmente na conexão:  
  
-   Se nenhum driver estiver carregado na conexão, o Driver Manager verifica se o driver especificado está carregado em outra conexão no mesmo ambiente. Caso assim, o Driver Manager carregue o driver na conexão e ligue para **o SQLAllocHandle** no driver com a opção SQL_HANDLE_ENV.  
  
     O Driver Manager então chama **SQLAllocHandle** no driver com a opção SQL_HANDLE_DBC, mesmo que ele tenha sido ou não carregado. Se o aplicativo definir quaisquer atributos de conexão, o Driver Manager chamará **SQLSetConnectAttr** no driver; se ocorrer um erro, a função de conexão do Driver Manager retorna o SQLSTATE IM006 (falha do **SQLSetConnectAttr** do driver). Finalmente, o Driver Manager chama a função de conexão no driver.  
  
-   Se o driver especificado estiver carregado na conexão, o Gerenciador de drivers chamará apenas a função de conexão no driver. Neste caso, o driver deve certificar-se de que todos os atributos de conexão na conexão mantenham suas configurações atuais.  
  
-   Se um driver diferente estiver carregado na conexão, o Driver Manager chamará **o SQLFreeHandle** no driver para liberar a conexão. Se não houver outras conexões que utilizem o driver, o Driver Manager chama **o SQLFreeHandle** no driver para liberar o ambiente e descarregar o motorista. Em seguida, o Driver Manager executa as mesmas operações que quando um driver não é carregado na conexão.  
  
 O Driver Manager bloqueará a alça do ambiente *(henv)* antes de chamar o **SQLAllocHandle** e **o SQLFreeHandle** do driver quando *o HandleType* estiver definido como **SQL_HANDLE_DBC**.  
  
 Quando o aplicativo chama **SQLDisconnect,** o Driver Manager chama **SQLDisconnect** no driver. No entanto, deixa o motorista carregado caso o aplicativo se reconecte ao motorista. Quando o aplicativo chama **sqlfreehandle** com a opção SQL_HANDLE_DBC, o Gerenciador de driver chama **SQLFreeHandle** no driver. Se o driver não for usado por outras conexões, o Driver Manager então chamará **SQLFreeHandle** no driver com a opção SQL_HANDLE_ENV e descarregará o motorista.
