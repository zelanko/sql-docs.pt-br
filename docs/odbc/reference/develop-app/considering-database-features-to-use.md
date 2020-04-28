---
title: Considerando os recursos de banco de dados a serem usados | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9d966781def1c3eab6a9568eab07ab591326171
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299006"
---
# <a name="considering-database-features-to-use"></a>Considerar os recursos de banco de dados a serem usados
Depois que o nível básico de interoperabilidade é conhecido, os recursos de banco de dados usados pelo aplicativo devem ser considerados. Por exemplo, quais instruções SQL serão executadas pelo aplicativo? O aplicativo usará cursores roláveis? Transações? Aos? Dados longos? Para obter ideias sobre quais recursos podem não ser suportados por todos os DBMSs, consulte as descrições da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)e [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) e o [Apêndice C: SQL Grammar](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Os recursos exigidos por um aplicativo podem eliminar alguns DBMSs da lista de DBMSs de destino. Eles também podem mostrar que o aplicativo pode facilmente ter como alvo muitos DBMSs.  
  
 Por exemplo, se os recursos necessários forem simples, eles normalmente podem ser implementados com um alto grau de interoperabilidade. Um aplicativo que executa uma instrução **Select** simples e recupera os resultados com um cursor de somente avanço provavelmente será altamente interoperável devido à sua simplicidade: quase todos os drivers e DBMSs dão suporte à funcionalidade necessária.  
  
 No entanto, se os recursos necessários forem mais complexos, como cursores roláveis, instruções de atualização e exclusão posicionadas e procedimentos, as compensações devem ser feitas com frequência. Há várias possibilidades:  
  
-   **Menor interoperabilidade, mais recursos.** O aplicativo inclui os recursos, mas funciona apenas com DBMSs que dão suporte a eles.  
  
-   **Maior interoperabilidade, menos recursos.** O aplicativo descarta os recursos, mas funciona com mais DBMSs.  
  
-   **Maior interoperabilidade, recursos opcionais.** O aplicativo inclui os recursos, mas os torna disponíveis somente com os DBMSs que dão suporte a eles.  
  
-   **Maior interoperabilidade, mais recursos.** O aplicativo usa os recursos com DBMSs que dão suporte a eles e os emula para DBMSs que não têm.  
  
 Os dois primeiros casos são relativamente simples de implementar, pois os recursos são usados com todos os DBMS com suporte ou com nenhum. Os dois últimos casos, por outro lado, são mais complexos. É necessário em ambos os casos para verificar se o DBMS dá suporte aos recursos e, no último caso, para gravar uma quantidade potencialmente grande de código para emular esses recursos. Portanto, esses esquemas provavelmente exigirão mais tempo de desenvolvimento e poderão ser mais lentos no tempo de execução.  
  
 Considere um aplicativo de consulta genérico que possa se conectar a uma única fonte de dados. O aplicativo aceita uma consulta do usuário e exibe os resultados em uma janela. Agora suponha que esse aplicativo tenha um recurso que permita aos usuários exibir os resultados de várias consultas simultaneamente. Ou seja, eles podem executar uma consulta e examinar alguns dos resultados, executar uma consulta diferente e examinar alguns de seus resultados e retornar à primeira consulta. Isso apresenta um problema de interoperabilidade porque alguns drivers dão suporte a apenas uma única instrução ativa.  
  
 O aplicativo tem várias opções, com base no que o driver retorna para a opção de SQL_MAX_CONCURRENT_ACTIVITIES em **SQLGetInfo**:  
  
-   **Sempre dê suporte a várias consultas.** Depois de se conectar a um driver, o aplicativo verifica o número de instruções ativas. Se o driver oferecer suporte a apenas uma instrução ativa, o aplicativo fechará a conexão e informará ao usuário que o driver não oferece suporte à funcionalidade necessária. O aplicativo é fácil de implementar e tem funcionalidade completa, mas tem uma interoperabilidade inferior.  
  
-   **Nunca há suporte para várias consultas.** O aplicativo descarta completamente o recurso. É fácil de implementar e tem alta interoperabilidade, mas tem menos funcionalidade.  
  
-   **Dar suporte a várias consultas somente se o driver tiver.** Depois de se conectar a um driver, o aplicativo verifica o número de instruções ativas. O aplicativo permite que o usuário inicie uma nova instrução quando uma já estiver ativa somente se o driver oferecer suporte a várias instruções ativas. O aplicativo tem funcionalidade e interoperabilidade maiores, mas é mais difícil de implementar.  
  
-   **Sempre dê suporte a várias consultas e emule-as quando necessário.** Depois de se conectar a um driver, o aplicativo verifica o número de instruções ativas. O aplicativo sempre permite que o usuário inicie uma nova instrução quando uma já estiver ativa. Se o driver oferecer suporte a apenas uma instrução ativa, o aplicativo abrirá uma conexão adicional com esse driver e executará a nova instrução nessa conexão. O aplicativo tem funcionalidade completa e alta interoperabilidade, mas é mais difícil de implementar.
