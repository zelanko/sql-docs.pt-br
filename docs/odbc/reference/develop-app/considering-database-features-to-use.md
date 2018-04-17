---
title: Considerando os recursos de banco de dados para uso | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], database features
ms.assetid: 59760114-508e-46c5-81d2-8f2498c0d778
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a980d3f10b95af3f75945ad945bd5afd78ed5edf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="considering-database-features-to-use"></a>Considerando os recursos de banco de dados de uso
Depois que o nível básico de interoperabilidade for conhecido, os recursos de banco de dados usados pelo aplicativo devem ser considerados. Por exemplo, quais instruções SQL de aplicativo executará? O aplicativo irá usar cursores roláveis? Transações? Procedimentos? Dados Long? Para obter ideias sobre quais recursos talvez não tenha suporte por todos os DBMSs, consulte o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), e [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) edescriçõesdefunção[ Apêndice c: gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Os recursos necessários para um aplicativo podem eliminar alguns DBMSs da lista de destino DBMSs. Eles também podem mostrar que o aplicativo pode direcionar facilmente DBMSs muitos.  
  
 Por exemplo, se os recursos necessários são simples, eles geralmente podem ser implementados com um alto grau de interoperabilidade. Um aplicativo que executa uma simples **selecione** instrução e recupera os resultados com um cursor somente de avanço é provável de ser altamente interoperável por meio de sua simplicidade: quase todos os drivers e DBMSs oferece suporte à funcionalidade-lo necessidades.  
  
 No entanto, se os recursos necessários são mais complexos, como cursores roláveis e procedimentos e instruções delete e atualização posicionada, compensações devem geralmente ser feitas. Há várias possibilidades:  
  
-   **Interoperabilidade menor, mais recursos.** O aplicativo inclui os recursos, mas funciona somente com os que dão suporte a eles.  
  
-   **Interoperabilidade mais alta, menos recursos.** O aplicativo descarta os recursos, mas funciona com DBMSs mais.  
  
-   **Interoperabilidade superior, os recursos opcionais.** O aplicativo inclui os recursos, mas disponibiliza apenas com esses DBMSs que dão suporte a eles.  
  
-   **Interoperabilidade maior, mais recursos.** O aplicativo usa os recursos com os que dão suporte a eles e emula-los para os que não.  
  
 Os dois primeiros casos são relativamente simples de implementar, porque os recursos são usados com todos os DBMSs com suporte ou none. Por outro lado, os dois últimos casos, são mais complexos. É necessário em ambos os casos para verificar se o DBMS for compatível com os recursos e no último caso para gravar uma potencialmente grande quantidade de código para emular esses recursos. Portanto, esses esquemas provavelmente exigirão mais tempo de desenvolvimento e poderão ser mais lentos em tempo de execução.  
  
 Considere um aplicativo de consulta genérico que pode se conectar a uma fonte de dados. O aplicativo aceita uma consulta do usuário e exibe os resultados em uma janela. Agora suponha que este aplicativo possui um recurso que permite que os usuários exibem os resultados de várias consultas simultaneamente. Ou seja, eles podem executar uma consulta e examinar alguns dos resultados, execute uma consulta diferente examinar alguns de seus resultados e, em seguida, retornar para a primeira consulta. Isso apresenta um problema de interoperabilidade porque alguns drivers de suportam a apenas uma única instrução ativa.  
  
 O aplicativo tem um número de opções, com base no qual o driver retorna para a opção SQL_MAX_CONCURRENT_ACTIVITIES **SQLGetInfo**:  
  
-   **Suporte a várias consultas sempre.** Depois de se conectar a um driver, o aplicativo verifica o número de instruções ativas. Se o driver oferece suporte a apenas uma instrução ativa, o aplicativo fecha a conexão e informa ao usuário que o driver não oferece suporte à funcionalidade necessária. O aplicativo é fácil de implementar e tem a funcionalidade completa, mas tem interoperabilidade inferior.  
  
-   **Nunca oferecem suporte a várias consultas.** O aplicativo descarta o recurso completamente. Ele é fácil de implementar e tem alta interoperabilidade mas tem menos funcionalidade.  
  
-   **Suporte a várias consultas apenas se o driver.** Depois de se conectar a um driver, o aplicativo verifica o número de instruções ativas. O aplicativo permite que o usuário iniciar uma nova instrução quando uma já está ativa somente se o driver dá suporte a várias instruções ativas. O aplicativo tem maior funcionalidade e interoperabilidade, mas é mais difícil de implementar.  
  
-   **Sempre dá suporte a várias consultas e emulá-los quando necessário.** Depois de se conectar a um driver, o aplicativo verifica o número de instruções ativas. O aplicativo sempre permite que o usuário iniciar uma nova instrução quando um já está ativo. Se o driver oferece suporte a apenas uma instrução ativa, o aplicativo abre uma conexão adicional para esse driver e executa a nova instrução em que a conexão. O aplicativo tem total funcionalidade e interoperabilidade alta, mas é mais difícil de implementar.
