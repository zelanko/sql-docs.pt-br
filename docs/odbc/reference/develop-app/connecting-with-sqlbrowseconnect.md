---
title: Conectando-se com o SQLBrowseConnect | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4d738d394bb3c507f6aa08f736016b51ac4fefb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294656"
---
# <a name="connecting-with-sqlbrowseconnect"></a>Conectar-se com o SQLBrowseConnect
**SQLBrowseConnect**, como **SQLDriverConnect,** usa uma seqüência de conexão. No entanto, usando **o SQLBrowseConnect,** um aplicativo pode construir uma seqüência de conexão completa no tempo de execução. Isso permite que o aplicativo faça duas tarefas:  
  
-   Construa suas próprias caixas de diálogo para solicitar essas informações, mantendo assim o controle sobre sua "aparência".  
  
-   Procure no sistema por fontes de dados que possam ser usadas por um driver específico, possivelmente em várias etapas. Por exemplo, primeiro o usuário pode procurar servidores na rede e, depois de escolher um, procurar no servidor pelos bancos de dados acessíveis pelo driver.  
  
 O aplicativo chama **o SQLBrowseConnect** e passa uma seqüência de conexões, conhecida como *string de conexão de solicitação de navegação,* que especifica um driver ou fonte de dados. O driver retorna uma seqüência de conexões, conhecida como *string de conexão de resultado de navegação,* que contém palavras-chave, valores possíveis (se a palavra-chave aceitar um conjunto discreto de valores) e nomes fáceis de usar. O aplicativo constrói uma caixa de diálogo com os nomes fáceis de usar e solicita valores ao usuário. Em seguida, ele cria uma nova seqüência de conexão de solicitação de navegação a partir desses valores e retorna isso ao driver com outra chamada para **SQLBrowseConnect**.  
  
 Como as strings de conexão são passadas para frente e para trás, o driver pode fornecer vários níveis de navegação retornando uma nova seqüência de conexão quando o aplicativo retorna o antigo. Por exemplo, na primeira vez que um aplicativo chama **SQLBrowseConnect,** o driver pode retornar palavras-chave para solicitar ao usuário um nome de servidor. Quando o aplicativo retorna o nome do servidor, o driver pode retornar palavras-chave para solicitar ao usuário um banco de dados. O processo de navegação seria concluído após o aplicativo retornar o nome do banco de dados.  
  
 Cada vez que **o SQLBrowseConnect** retorna uma nova seqüência de conexão de resultados de navegação, ele retorna SQL_NEED_DATA como seu código de retorno. Isso diz ao aplicativo que o processo de conexão não está completo. Até **que o SQLBrowseConnect retorne** SQL_SUCCESS, a conexão está em um estado de Dados de Necessidade e não pode ser usada para outros fins, como definir um atributo de conexão. O aplicativo pode encerrar o processo de navegação de conexão ligando para **SQLDisconnect**.  
  
 Esta seção contém o seguinte tópico.  
  
-   [Exemplo de navegação do SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
