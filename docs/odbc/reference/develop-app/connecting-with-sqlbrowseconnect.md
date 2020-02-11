---
title: Conectando-se ao SQLBrowseConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLBrowseConnect
- SQLBrowseConnect function [ODBC], connecting
- connecting to data source [ODBC], SQLBrowseConnect
ms.assetid: 6c2e9f76-b766-48df-b109-246bb05ae45d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04df089b97bf385925c87a98b3f89cdac3ef21e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083129"
---
# <a name="connecting-with-sqlbrowseconnect"></a>Conectar-se com o SQLBrowseConnect
**SQLBrowseConnect**, como **SQLDriverConnect**, usa uma cadeia de conexão. No entanto, usando **SQLBrowseConnect**, um aplicativo pode construir uma cadeia de conexão completa em tempo de execução. Isso permite que o aplicativo faça duas tarefas:  
  
-   Crie suas próprias caixas de diálogo para solicitar essas informações, retendo assim o controle sobre sua "aparência".  
  
-   Procure no sistema por fontes de dados que possam ser usadas por um driver específico, possivelmente em várias etapas. Por exemplo, primeiro o usuário pode procurar servidores na rede e, depois de escolher um, procurar no servidor pelos bancos de dados acessíveis pelo driver.  
  
 O aplicativo chama **SQLBrowseConnect** e passa uma cadeia de conexão, conhecida como a *cadeia de conexão de solicitação de procura,* que especifica um driver ou uma fonte de dados. O driver retorna uma cadeia de conexão, conhecida como a *cadeia de conexão de resultado de procura,* que contém palavras-chave, valores possíveis (se a palavra-chave aceitar um conjunto discreto de valores) e nomes amigáveis. O aplicativo cria uma caixa de diálogo com os nomes amigáveis do usuário e solicita valores ao usuário. Em seguida, ele cria uma nova cadeia de conexão de solicitação de procura com base nesses valores e retorna isso ao driver com outra chamada para **SQLBrowseConnect**.  
  
 Como as cadeias de conexão são passadas para frente e para trás, o driver pode fornecer vários níveis de navegação, retornando uma nova cadeia de conexão quando o aplicativo retorna o antigo. Por exemplo, na primeira vez que um aplicativo chama **SQLBrowseConnect**, o driver pode retornar palavras-chave para solicitar ao usuário um nome de servidor. Quando o aplicativo retorna o nome do servidor, o driver pode retornar palavras-chave para solicitar ao usuário um banco de dados. O processo de navegação seria concluído depois que o aplicativo retornasse o nome do banco de dados.  
  
 Cada vez que **SQLBrowseConnect** retorna uma nova cadeia de conexão de resultado de procura, ela retorna SQL_NEED_DATA como seu código de retorno. Isso informa ao aplicativo que o processo de conexão não está completo. Até que **SQLBrowseConnect** retorne SQL_SUCCESS, a conexão estará em um estado de dados necessário e não poderá ser usada para outras finalidades, como para definir um atributo de conexão. O aplicativo pode encerrar o processo de navegação de conexão chamando **SQLDisconnect**.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Exemplo de navegação do SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
