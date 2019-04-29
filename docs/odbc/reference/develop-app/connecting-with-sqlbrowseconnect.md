---
title: Conectando com SQLBrowseConnect | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ec1cd42e6704bc5168b1eb20841100fc279a66ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042762"
---
# <a name="connecting-with-sqlbrowseconnect"></a>Conectar-se com o SQLBrowseConnect
**SQLBrowseConnect**, como **SQLDriverConnect**, usa uma cadeia de caracteres de conexão. No entanto, usando **SQLBrowseConnect**, um aplicativo pode construir uma cadeia de caracteres de conexão completa no tempo de execução. Isso permite que o aplicativo faça duas tarefas:  
  
-   Criar suas próprias caixas de diálogo para solicitar essas informações, assim mantendo o controle sobre seu "aparência."  
  
-   Procure no sistema por fontes de dados que possam ser usadas por um driver específico, possivelmente em várias etapas. Por exemplo, primeiro o usuário pode procurar servidores na rede e, depois de escolher um, procurar no servidor pelos bancos de dados acessíveis pelo driver.  
  
 O aplicativo chama **SQLBrowseConnect** e passa uma cadeia de caracteres de conexão, conhecida como o *procurar a cadeia de caracteres de conexão de solicitação,* que especifica uma driver ou fonte de dados. O driver retorna uma cadeia de caracteres de conexão, conhecida como o *procure a cadeia de caracteres de conexão do resultado,* que contém palavras-chave, os valores possíveis (se a palavra-chave aceita um conjunto discreto de valores) e nomes amigáveis. O aplicativo cria uma caixa de diálogo com os nomes amigáveis e solicita ao usuário para valores. Em seguida, cria uma nova cadeia de conexão de solicitação de procurar esses valores e retorna isso para o driver com outra chamada para **SQLBrowseConnect**.  
  
 Como cadeias de caracteres de conexão são passadas de e para trás, o driver pode fornecer vários níveis de navegação, retornando uma nova cadeia de caracteres de conexão quando o aplicativo antigo é retornado. Por exemplo, na primeira vez em que um aplicativo chama **SQLBrowseConnect**, o driver pode retornar palavras-chave para solicitar ao usuário para um nome de servidor. Quando o aplicativo retorna o nome do servidor, o driver pode retornar palavras-chave para solicitar ao usuário para um banco de dados. O processo de localização seria concluído depois que o aplicativo retornou o nome do banco de dados.  
  
 Cada vez **SQLBrowseConnect** retorna uma nova cadeia de conexão de resultado procurar, ele retornará SQL_NEED_DATA como seu código de retorno. Isso informa o aplicativo que o processo de conexão não foi concluído. Até que **SQLBrowseConnect** retorna SQL_SUCCESS, a conexão está em um estado de dados precisa e não pode ser usada para outras finalidades, como definir um atributo de conexão. O aplicativo pode encerrar a conexão navegando o processo chamando **SQLDisconnect**.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Exemplo de navegação do SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
