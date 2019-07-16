---
title: Considerando os recursos de banco de dados para uso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], database features
ms.assetid: 59760114-508e-46c5-81d2-8f2498c0d778
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3a945eef43a1fc12689853c3fa209f6126df4f0d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951879"
---
# <a name="considering-database-features-to-use"></a>Considerar os recursos de banco de dados a serem usados
Depois que o nível básico de interoperabilidade é conhecido, os recursos de banco de dados usados pelo aplicativo devem ser considerados. Por exemplo, quais instruções SQL o aplicativo executará? O aplicativo usará cursores roláveis? Transações? Procedimentos? Dados Long? Para sugestões sobre quais recursos podem não ter suporte por todos os DBMSs, consulte o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), e [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) edescriçõesdefunção[ Apêndice c: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Os recursos necessários para um aplicativo podem eliminar alguns DBMSs da lista de destino DBMSs. Eles também podem mostrar que o aplicativo pode direcionar facilmente muitos DBMSs.  
  
 Por exemplo, se os recursos necessários são simples, eles geralmente podem ser implementados com um alto grau de interoperabilidade. Um aplicativo que executa um simples **selecionar** instrução e recupera resultados com um cursor somente de avanço é provavelmente será altamente interoperável em virtude de sua simplicidade: Quase todos os drivers e DBMSs suportam a funcionalidade que ele precisa.  
  
 No entanto, se os recursos necessários são mais complexos, como atualização posicionada, cursores roláveis e instruções delete e procedimentos, compensações devem normalmente ser feitas. Existem várias possibilidades:  
  
-   **Interoperabilidade de menor, mais recursos.** O aplicativo inclui os recursos, mas funciona somente com DBMSs que dão suporte a eles.  
  
-   **Maior interoperabilidade, menos recursos.** O aplicativo descarta os recursos, mas funciona com mais DBMSs.  
  
-   **Maior interoperabilidade, recursos opcionais.** O aplicativo inclui os recursos, mas torna-os disponíveis apenas com esses DBMSs que dão suporte a eles.  
  
-   **Interoperabilidade maior, mais recursos.** O aplicativo usa os recursos com DBMSs que dão suporte a eles e emula-los para os que não têm.  
  
 Os dois primeiros casos são relativamente simples de implementar, porque os recursos são usados com todos os DBMSs com suporte ou com nenhum. Os dois últimos casos, por outro lado, são mais complexos. É necessário em ambos os casos para verificar se o DBMS der suporte a recursos e no último caso, para gravar uma potencialmente grande quantidade de código para emular a esses recursos. Portanto, esses esquemas têm probabilidade de exigir mais tempo de desenvolvimento e poderão ser mais lentos em tempo de execução.  
  
 Considere um aplicativo de consulta genérico que pode se conectar a uma fonte de dados. O aplicativo aceita uma consulta do usuário e exibe os resultados em uma janela. Agora suponha que esse aplicativo tem um recurso que permite aos usuários exibir os resultados de várias consultas simultaneamente. Ou seja, eles podem executar uma consulta e examinar alguns dos resultados, execute uma consulta diferente e examinar alguns dos seus resultados e, em seguida, retornar para a primeira consulta. Isso apresenta um problema de interoperabilidade porque alguns drivers dá suporte a apenas uma única instrução ativa.  
  
 O aplicativo tem uma série de opções, com base no qual o driver retornará para a opção SQL_MAX_CONCURRENT_ACTIVITIES na **SQLGetInfo**:  
  
-   **Sempre dão suporte a várias consultas.** Depois de se conectar a um driver, o aplicativo verifica o número de instruções ativas. Se o driver dá suporte a apenas uma instrução ativa, o aplicativo fecha a conexão e informará ao usuário que o driver não dá suporte a funcionalidade necessária. O aplicativo é fácil de implementar e tem a funcionalidade completa, mas tem menor interoperabilidade.  
  
-   **Suporte a várias consultas nunca.** O aplicativo descarta o recurso completamente. Ele é fácil de implementar e tem um alto nível de interoperabilidade, mas tem menos funcionalidade.  
  
-   **Suporte a várias consultas apenas se o driver faz.** Depois de se conectar a um driver, o aplicativo verifica o número de instruções ativas. O aplicativo permite ao usuário iniciar uma nova instrução, quando um já está ativo somente se o driver dá suporte a várias instruções ativas. O aplicativo tem maior funcionalidade e interoperabilidade, mas é mais difícil de implementar.  
  
-   **Sempre dá suporte a várias consultas e emulá-los quando necessário.** Depois de se conectar a um driver, o aplicativo verifica o número de instruções ativas. O aplicativo sempre permite ao usuário iniciar uma nova instrução, quando um já está ativo. Se o driver dá suporte a apenas uma instrução ativa, o aplicativo abre uma conexão adicional para esse driver e executa a instrução de novo nessa conexão. O aplicativo tem a funcionalidade completa e alto nível de interoperabilidade, mas é mais difícil de implementar.
