---
title: Considerando os recursos do banco de dados para usar | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299006"
---
# <a name="considering-database-features-to-use"></a>Considerar os recursos de banco de dados a serem usados
Depois que o nível básico de interoperabilidade for conhecido, os recursos de banco de dados utilizados pelo aplicativo devem ser considerados. Por exemplo, quais instruções SQL o aplicativo executará? O aplicativo usará cursores roláveis? Transações? Procedimentos? Dados longos? Para obter ideias sobre quais recursos podem não ser suportados por todos os DBMSs, consulte as descrições da função [SQLGetInfo,](../../../odbc/reference/syntax/sqlgetinfo-function.md) [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)e [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) e [o apêndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Os recursos exigidos por um aplicativo podem eliminar alguns DBMSs da lista de DBMSs de destino. Eles também podem mostrar que o aplicativo pode facilmente atingir muitos DBMSs.  
  
 Por exemplo, se os recursos necessários são simples, eles geralmente podem ser implementados com um alto grau de interoperabilidade. Um aplicativo que executa uma simples instrução **SELECT** e recupera resultados com um cursor somente para frente provavelmente será altamente interoperável em virtude de sua simplicidade: Quase todos os drivers e DBMSs suportam a funcionalidade que precisa.  
  
 No entanto, se os recursos necessários forem mais complexos, como cursores roláveis, instruções de atualização e exclusão posicionadas e procedimentos, as trocas devem ser feitas muitas vezes. Existem várias possibilidades:  
  
-   **Menor interoperabilidade, mais recursos.** O aplicativo inclui os recursos, mas funciona apenas com DBMSs que os suportam.  
  
-   **Maior interoperabilidade, menos recursos.** O aplicativo descarta os recursos, mas funciona com mais DBMSs.  
  
-   **Maior interoperabilidade, características opcionais.** O aplicativo inclui os recursos, mas os disponibiliza apenas com os DBMSs que os suportam.  
  
-   **Maior interoperabilidade, mais recursos.** O aplicativo usa os recursos com DBMSs que os suportam e os emula para DBMSs que não o fazem.  
  
 Os dois primeiros casos são relativamente simples de implementar, porque os recursos são usados com todos os DBMS suportados ou sem nenhum. Os dois últimos casos, por outro lado, são mais complexos. Em ambos os casos, é necessário verificar se o DBMS suporta os recursos e, no último caso, escrever uma quantidade potencialmente grande de código para emular esses recursos. Portanto, esses esquemas provavelmente exigirão mais tempo de desenvolvimento e podem ser mais lentos no tempo de execução.  
  
 Considere um aplicativo de consulta genérico que pode se conectar a uma única fonte de dados. O aplicativo aceita uma consulta do usuário e exibe os resultados em uma janela. Agora suponha que este aplicativo tenha um recurso que permite que os usuários exibam os resultados de várias consultas simultaneamente. Ou seja, eles podem executar uma consulta e olhar para alguns dos resultados, executar uma consulta diferente e olhar para alguns de seus resultados e, em seguida, retornar à primeira consulta. Isso apresenta um problema de interoperabilidade porque alguns drivers suportam apenas uma única declaração ativa.  
  
 O aplicativo tem uma série de opções, com base no que o driver retorna para a opção SQL_MAX_CONCURRENT_ACTIVITIES no **SQLGetInfo**:  
  
-   **Sempre apoie várias consultas.** Depois de conectar-se a um driver, o aplicativo verifica o número de declarações ativas. Se o driver suportar apenas uma declaração ativa, o aplicativo fecha a conexão e informa ao usuário que o driver não suporta a funcionalidade necessária. O aplicativo é fácil de implementar e tem funcionalidade completa, mas tem menor interoperabilidade.  
  
-   **Nunca suporte várias consultas.** O aplicativo descarta o recurso completamente. É fácil de implementar e tem alta interoperabilidade, mas tem menos funcionalidade.  
  
-   **Suporte várias consultas somente se o driver o fizer.** Depois de conectar-se a um driver, o aplicativo verifica o número de declarações ativas. O aplicativo permite que o usuário inicie uma nova instrução quando um já está ativo apenas se o driver suportar várias instruções ativas. O aplicativo tem maior funcionalidade e interoperabilidade, mas é mais difícil de implementar.  
  
-   **Sempre apoie várias consultas e emule-as quando necessário.** Depois de conectar-se a um driver, o aplicativo verifica o número de declarações ativas. O aplicativo sempre permite que o usuário inicie uma nova declaração quando um já está ativo. Se o driver suportar apenas uma declaração ativa, o aplicativo abrirá uma conexão adicional com esse driver e executará a nova declaração sobre essa conexão. O aplicativo tem funcionalidade completa e alta interoperabilidade, mas é mais difícil de implementar.
