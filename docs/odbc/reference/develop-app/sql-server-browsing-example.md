---
description: Exemplo de navegação do SQL Server
title: Exemplo de navegação de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14016832989c6fcba1dc39bc64434e72b049c18a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424558"
---
# <a name="sql-server-browsing-example"></a>Exemplo de navegação do SQL Server
O exemplo a seguir mostra como **SQLBrowseConnect** pode ser usado para procurar as conexões disponíveis com um driver para SQL Server. Primeiro, o aplicativo solicita um identificador de conexão:  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 Em seguida, o aplicativo chama **SQLBrowseConnect** e especifica o driver de SQL Server, usando a descrição do driver retornada pelos **sqldriveers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Como essa é a primeira chamada para **SQLBrowseConnect**, o Gerenciador de driver carrega o driver SQL Server e chama a função **SQLBrowseConnect** do driver com os mesmos argumentos recebidos do aplicativo.  
  
> [!NOTE]  
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, especifique `Trusted_Connection=yes` o lugar das informações de ID de usuário e senha na cadeia de conexão.  
  
 O driver determina que esta é a primeira chamada para **SQLBrowseConnect** e retorna o segundo nível de atributos de conexão: servidor, nome de usuário, senha, nome do aplicativo e ID da estação de trabalho. Para o atributo de servidor, ele retorna uma lista de nomes de servidor válidos. O código de retorno de **SQLBrowseConnect** é SQL_NEED_DATA. Aqui está a cadeia de caracteres de resultado da procura:  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 Cada palavra-chave na cadeia de caracteres de resultado da procura é seguida por dois-pontos e uma ou mais palavras antes do sinal de igual. Essas palavras são o nome amigável que um aplicativo pode usar para criar uma caixa de diálogo. As palavras-chave **aplicativo** e **WSID** são prefixadas por um asterisco, o que significa que elas são opcionais. As palavras-chave **Server**, **UID**e **pwd** não são prefixadas por um asterisco; os valores devem ser fornecidos para eles na próxima procura da cadeia de caracteres da solicitação. O valor da palavra-chave **Server** pode ser um dos servidores retornados por **SQLBrowseConnect** ou um nome fornecido pelo usuário.  
  
 O aplicativo chama **SQLBrowseConnect** novamente, especificando o servidor verde e omitindo as palavras-chave do **aplicativo** e do **WSID** e os nomes amigáveis do usuário após cada palavra-chave:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 O driver tenta se conectar ao servidor verde. Se houver erros não fatais, como um par de valor de palavra-chave ausente, **SQLBrowseConnect** retornará SQL_NEED_DATA e permanecerá no mesmo estado que era anterior ao erro. O aplicativo pode chamar **SQLGetDiagField** ou **SQLGetDiagRec** para determinar o erro. Se a conexão for bem-sucedida, o driver retornará SQL_NEED_DATA e retornará a cadeia de caracteres de resultado de procura:  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 Como os atributos nessa cadeia de caracteres são opcionais, o aplicativo pode omiti-los. No entanto, o aplicativo deve chamar **SQLBrowseConnect** novamente. Se o aplicativo optar por omitir o nome do banco de dados e o idioma, ele especificará uma cadeia de caracteres de solicitação de procura vazia. Neste exemplo, o aplicativo escolhe o banco de dados pubs e chama **SQLBrowseConnect** uma hora final, omitindo a palavra-chave **Language** e o asterisco antes da palavra-chave **Database** :  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Como o atributo de **banco de dados** é o atributo de conexão final exigido pelo driver, o processo de navegação é concluído, o aplicativo é conectado à fonte de dados e **SQLBrowseConnect** retorna SQL_SUCCESS. **SQLBrowseConnect** também retorna a cadeia de conexão completa como a cadeia de caracteres de resultado da procura:  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 A cadeia de conexão final retornada pelo driver não contém os nomes amigáveis do usuário após cada palavra-chave, nem contém palavras-chave opcionais não especificadas pelo aplicativo. O aplicativo pode usar essa cadeia de caracteres com **SQLDriverConnect** para reconectar-se à fonte de dados no identificador de conexão atual (depois de desconectar) ou para se conectar à fonte de dados em um identificador de conexão diferente. Por exemplo:  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
