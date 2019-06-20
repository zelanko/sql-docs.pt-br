---
title: Cursores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- results [SQL Server], cursors
- Transact-SQL cursors, about cursors
- cursors [SQL Server]
- data access [SQL Server], cursors
- result sets [SQL Server], cursors
- requesting cursors
- cursors [SQL Server], about cursors
ms.assetid: e668b40c-bd4d-4415-850d-20fc4872ee72
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8123179285b94377fff758121f535175705f29af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62918687"
---
# <a name="cursors"></a>Cursores
  As operações em um ato de banco de dados relacional em um conjunto completo de linhas. Por exemplo, o conjunto de linhas retornado por uma instrução SELECT consiste de todas as linhas que satisfazem as condições na cláusula WHERE da instrução. Este conjunto completo de linhas retornado pela instrução é conhecido como conjunto de resultados. Aplicativos, especialmente aplicativos online interativos, não podem sempre trabalhar efetivamente com todo o conjunto de resultados como uma unidade. Esses aplicativos precisam de um mecanismo para trabalhar com uma linha ou um bloco pequeno de linhas de cada vez. Os cursores são uma extensão dos conjuntos de resultados que proveem esse mecanismo.  
  
 Os cursores estendem o resultado de processamento por:  
  
-   Permitirem o posicionamento em linhas específicas do conjunto de resultados.  
  
-   Recuperarem uma linha ou bloco de linhas de posições atuais em um conjunto de resultados.  
  
-   Oferecerem suporte às modificações de dados nas linhas da posição atual no conjunto de resultados.  
  
-   Oferecerem suporte a diferentes níveis de visibilidade às mudanças feitas por outros usuários ao banco de dados que são apresentados no conjunto de resultados.  
  
-   Fornecerem instruções [!INCLUDE[tsql](../includes/tsql-md.md)] em scripts, procedimentos armazenados, e acionarem o acesso de gatilho aos dados em um conjunto de resultados.  
  
## <a name="concepts"></a>Conceitos  
 Implementações de cursor  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dá suporte a três implementações de cursor.  
  
 cursores Transact-SQL  
 Baseiam-se na sintaxe DECLARE CURSOR e são usados principalmente nos scripts [!INCLUDE[tsql](../includes/tsql-md.md)] , procedimentos armazenados e disparadores. [!INCLUDE[tsql](../includes/tsql-md.md)] os cursores são implementados no servidor e gerenciados pelas instruções [!INCLUDE[tsql](../includes/tsql-md.md)] enviadas do cliente ao servidor. Eles também podem ser contidos em lotes, procedimentos armazenados ou gatilhos.  
  
 Cursores de servidor de API (interface de programação de aplicativo)  
 Dão suporte a funções de cursor API no OLE DB e ODBC. Cursores de servidor API são implementados no servidor. Sempre que um aplicativo cliente chama uma função de cursor da API, o provedor OLE DB ou do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client ou o driver ODBC transmite a solicitação ao servidor para ação contra o cursor de servidor API.  
  
 Cursores do cliente  
 São implementados internamente pelo driver ODBC do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client e pela DLL que implementa a API do ADO. Cursores do cliente são implementados fazendo o cache de todas as linhas do conjunto de resultados no cliente. Sempre que um aplicativo cliente chama uma função de cursor API, o driver ODBC do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client ou a DLL ADO executa a operação de cursor nas linhas do conjunto de resultados em cache no cliente.  
  
 Tipos de cursores  
 Somente avanço  
 Um cursor de somente avanço não dá suporte a rolagem; ele suporta apenas a busca das linhas em série do início ao término do cursor. As linhas não são recuperadas do banco de dados até que sejam buscadas. Os efeitos de todas as instruções INSERT, UPDATE e DELETE feitas pelo usuário atual ou confirmadas por outros usuários que afetam as linhas no conjunto de resultados são visíveis como as linhas buscadas pelo cursor.  
  
 Como o cursor não podem ser revertido, a maioria das alterações feitas nas linhas no banco de dados depois que a linha foi buscada não são visíveis pelo cursor. Nos casos em que um valor usado para determinar o local da linha dentro do conjunto de resultados é modificado, como a atualização de uma coluna coberta por um índice clusterizado, o valor modificado é visível pelo cursor.  
  
 Embora os modelos de cursor de API do banco de dados considerem um cursor de somente avanço um tipo distinto de cursor, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não faz isso. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] considera tanto somente de avanço quanto rolagem como opções que podem ser aplicadas a cursores estáticos, controlados por conjuntos de chaves e dinâmicos. [!INCLUDE[tsql](../includes/tsql-md.md)] os cursores dão suporte a cursores estáticos somente de avanço, controlados por conjuntos de chaves e dinâmicos. Os modelos de cursor de API de banco de dados assumem que os cursores estáticos, controlados por conjunto de chaves e dinâmicos são sempre roláveis. Quando um atributo ou propriedade de cursor de API de banco de dados é definido como somente de avanço, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o implementa como um cursor dinâmico somente de avanço.  
  
 Estático  
 O conjunto completo de resultados de um cursor estático é criado em **tempdb** quando o cursor está aberto. Um cursor estático sempre exibe o conjunto de resultados como ele estava quando o cursor estava aberto. Os cursores estáticos detectam poucas ou nenhuma alteração, porém consomem relativamente poucos recursos durante a rolagem.  
  
 O cursor não reflete qualquer mudança feita no banco de dados que afeta a associação do conjunto de resultados ou as alterações feitas nos valores nas colunas das linhas que compõem o conjunto de resultados. Um cursor estático não exibe novas linhas inseridas no banco de dados após o cursor ter sido aberto, mesmo se elas corresponderem aos critérios de pesquisa da instrução SELECT do cursor. Se as filas que constituem o conjunto de resultados forem atualizadas por outros usuários, os novos valores de dados não serão exibidos no cursor estático. O cursor estático exibe linhas excluídas do banco de dados após o cursor ter sido aberto. Nenhuma operação UPDATE, INSERT ou DELETE são refletidas em um cursor estático (a menos que o cursor esteja fechado e reaberto), nem mesmo alterações feitas usando a mesma conexão que abriu o cursor.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cursores estáticos são sempre somente leitura.  
  
 Como o conjunto de resultados de um cursor estático é armazenado em uma tabela de trabalho no **tempdb**, o tamanho das linhas do conjunto de resultados não pode exceder o tamanho máximo de linhas para uma tabela [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] usa o termo insensitive para cursores estáticos. Algum banco de dados APIs os identificam como cursores de instantâneo.  
  
 Keyset  
 A associação e a ordem de linhas em um cursor controlado por conjunto de chaves são fixadas quando o cursor é aberto. Os cursores controlados por conjuntos de chaves são controlados por um conjunto exclusivo de identificadores, as chaves, conhecido como conjunto de chaves. As chaves são criadas a partir de um conjunto de colunas, que identificam exclusivamente as linhas no conjunto de resultados. O conjunto de chaves é o conjunto dos valores de chaves de todas as linhas qualificadas para a instrução SELECT no momento em que o cursor foi aberto. O conjunto de chaves para um cursor controlado por conjunto de chaves é criado no **tempdb** quando o cursor é aberto.  
  
 Dinâmicos  
 Os cursores dinâmicos são o oposto dos cursores estáticos. Cursores dinâmicos refletem todas as alterações feitas nas linhas de seu conjunto de resultados ao rolar pelo cursor. Os valores de dados, a ordem e a associação das linhas do conjunto de resultados podem ser alterados em cada busca. Todas as instruções UPDATE, INSERT e DELETE feitas por todos os usuários são visíveis pelo cursor. As atualizações são visíveis imediatamente se forem feitas por meio do cursor usando uma função de API como **SQLSetPos** ou a cláusula [!INCLUDE[tsql](../includes/tsql-md.md)] WHERE CURRENT OF. As atualizações feitas fora do cursor não são visíveis até serem confirmadas, a menos que o nível de isolamento da transação do cursor esteja definido para ler não confirmadas. Planos de cursor dinâmicos nunca usam índices espaciais.  
  
## <a name="requesting-a-cursor"></a>Solicitando um cursor  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dá suporte a dois métodos de solicitação de cursor:  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)]  
  
     A linguagem [!INCLUDE[tsql](../includes/tsql-md.md)] oferece suporte a uma sintaxe para utilizar cursores modelados após a sintaxe de cursor ISO.  
  
-   Funções de cursor de interface de programação de aplicativo (API) de banco de dados  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dá suporte à funcionalidade do cursor dessas APIs de banco de dados:  
  
    -   ADO ([!INCLUDE[msCoName](../includes/msconame-md.md)] ActiveX Data Object)  
  
    -   OLE DB  
  
    -   ODBC (Open Database Connectivity)  
  
 Um aplicativo não deve nunca misturar estes dois métodos de solicitar um cursor. Um aplicativo que tenha usado um API para especificar comportamentos de cursor não deveria portanto executar uma instrução [!INCLUDE[tsql](../includes/tsql-md.md)] DECLARE CURSOR para também solicitar um cursor [!INCLUDE[tsql](../includes/tsql-md.md)] . Um aplicativo deve apenas executar DECLARE CURSOR se ele tiver retornado todos os atributos API do cursor de volta ao seu padrão.  
  
 Se não tiver havido uma solicitação de um cursor API, o [!INCLUDE[tsql](../includes/tsql-md.md)] , [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] padroniza para retornar um conjunto completo de resultados, conhecido como um conjunto padrão de resultados, para o aplicativo.  
  
## <a name="cursor-process"></a>Processo do cursor  
 [!INCLUDE[tsql](../includes/tsql-md.md)] cursores e cursores da API têm sintaxe diferente, mas o seguinte processo geral é usado com todos os cursores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] :  
  
1.  Associe um cursor ao conjunto de resultados de uma instrução [!INCLUDE[tsql](../includes/tsql-md.md)] e defina as características do cursor, tais como se as filas no cursor podem ser atualizadas ou não.  
  
2.  Execute a instrução [!INCLUDE[tsql](../includes/tsql-md.md)] para preencher o cursor.  
  
3.  Recupere as linhas no cursor que você quer visualizar. A operação para recuperar uma linha ou um bloco de linhas de um cursor é denominada busca. Executar uma série de buscas para recuperar linhas em direção para frente ou para trás é chamado rolagem.  
  
4.  Opcionalmente, execute operações de modificação (atualização ou exclusão) na fila da posição atual no cursor.  
  
5.  Feche o cursor.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Cursor Behaviors](native-client-odbc-cursors/cursor-behaviors.md) [How Cursors Are Implemented](native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
## <a name="see-also"></a>Consulte também  
 [DECLARE CURSOR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-cursor-transact-sql)   
 [Cursores &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/cursors-transact-sql)   
 [Funções de cursor &#40;Transact-SQL&#41;](/sql/t-sql/functions/cursor-functions-transact-sql)   
 [Procedimentos armazenados de cursor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql)  
  
  
