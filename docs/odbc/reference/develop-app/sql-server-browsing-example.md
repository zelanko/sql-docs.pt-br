---
title: Exemplo de navegação do servidor SQL | Microsoft Docs
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
ms.openlocfilehash: 7b15aa8e3d573660a312fceb5b9100a41f0384d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301977"
---
# <a name="sql-server-browsing-example"></a>Exemplo de navegação do SQL Server
O exemplo a seguir mostra como o **SQLBrowseConnect** pode ser usado para navegar nas conexões disponíveis com um driver para SQL Server. Primeiro, o aplicativo solicita uma alça de conexão:  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 Em seguida, o aplicativo chama **SQLBrowseConnect** e especifica o driver do SQL Server, usando a descrição do driver retornada por **SQLDrivers:**  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Como esta é a primeira chamada para **o SQLBrowseConnect,** o Driver Manager carrega o driver SQL Server e chama a função **SQLBrowseConnect** do driver com os mesmos argumentos recebidos do aplicativo.  
  
> [!NOTE]  
>  Se você estiver se conectando a um provedor de origem `Trusted_Connection=yes` de dados que suporta a autenticação do Windows, você deve especificar, em vez de Informações de ID do usuário e senha na seqüência de conexões.  
  
 O driver determina que esta é a primeira chamada para **SQLBrowseConnect** e retorna o segundo nível de atributos de conexão: servidor, nome de usuário, senha, nome do aplicativo e ID da estação de trabalho. Para o atributo do servidor, ele retorna uma lista de nomes de servidor válidos. O código de devolução do **SQLBrowseConnect** é SQL_NEED_DATA. Aqui está a seqüência de resultados da navegação:  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 Cada palavra-chave na seqüência de resultados de navegação é seguida por um cólon e uma ou mais palavras antes do sinal de igualdade. Essas palavras são o nome fácil de usar que um aplicativo pode usar para construir uma caixa de diálogo. As palavras-chave **APP** e **WSID** são prefixadas por um asterisco, o que significa que são opcionais. As palavras-chave **SERVER**, **UID**e **PWD** não são prefixadas por um asterisco; os valores devem ser fornecidos para eles na próxima seqüência de solicitação de navegação. O valor da palavra-chave **SERVER** pode ser um dos servidores retornados pelo **SQLBrowseConnect** ou um nome fornecido pelo usuário.  
  
 O aplicativo chama **o SQLBrowseConnect** novamente, especificando o servidor verde e omitindo as palavras-chave **APP** e **WSID** e os nomes fáceis de usar após cada palavra-chave:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 O driver tenta se conectar ao servidor verde. Se houver algum erro não fatal, como um par de valor de palavra-chave ausente, **o SQLBrowseConnect** retorna SQL_NEED_DATA e permanece no mesmo estado que estava antes do erro. O aplicativo pode ligar para **SQLGetDiagField** ou **SQLGetDiagRec** para determinar o erro. Se a conexão for bem sucedida, o driver retorna SQL_NEED_DATA e retorna a seqüência de resultados da navegação:  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 Como os atributos nesta seqüência são opcionais, o aplicativo pode omiti-los. No entanto, o aplicativo deve chamar **SQLBrowseConnect** novamente. Se o aplicativo optar por omitir o nome e o idioma do banco de dados, ele especificará uma seqüência de solicitações de navegação vazia. Neste exemplo, o aplicativo escolhe o banco de dados de pubs e chama **sqlBrowseConnect** uma última vez, omitindo a palavra-chave **LANGUAGE** e o asterisco antes da palavra-chave **BANCO DE DADOS:**  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Como o atributo **DATABASE** é o atributo final de conexão exigido pelo driver, o processo de navegação está concluído, o aplicativo está conectado à fonte de dados e o **SQLBrowseConnect** retorna SQL_SUCCESS. **O SQLBrowseConnect** também retorna a seqüência completa de conexões à medida que a seqüência de resultados de navegação:  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 A seqüência de conexão final retornada pelo driver não contém os nomes fáceis de usar após cada palavra-chave, nem contém palavras-chave opcionais não especificadas pelo aplicativo. O aplicativo pode usar essa string com **o SQLDriverConnect** para se reconectar à fonte de dados na alça de conexão atual (após a desconexão) ou para se conectar à fonte de dados em uma alça de conexão diferente. Por exemplo:  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
