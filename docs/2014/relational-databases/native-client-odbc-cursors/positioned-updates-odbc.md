---
title: Atualizações (ODBC) posicionadas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- SQLSetPos function
- SQLSetCursorName function
- ODBC applications, cursors
- cursors [ODBC], positioned updates
- positioned updates [ODBC]
- ODBC cursors, positioned updates
ms.assetid: ff404e02-630f-474d-b5d4-06442b756991
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2336944b583b6077d75bd5155bb4b52c66d9a852
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200525"
---
# <a name="positioned-updates-odbc"></a>Atualizações posicionadas (ODBC)
  O ODBC dá suporte a dois métodos para executar atualizações posicionadas em um cursor:  
  
-   **SQLSetPos**  
  
-   Cláusula WHERE CURRENT OF  
  
 A abordagem mais comum é usar **SQLSetPos**. Ela tem as seguintes opções:  
  
 SQL_POSITION  
 Posiciona o cursor ODBC em uma linha específica do conjunto de linhas atual.  
  
 SQL_REFRESH  
 Atualiza variáveis de programa associadas às colunas de conjunto de resultados com os valores da linha em que cursor está atualmente posicionado.  
  
 SQL_UPDATE  
 Atualiza a linha atual do cursor com os valores armazenados nas variáveis de programa associadas às colunas do conjunto de resultados.  
  
 SQL_DELETE  
 Exclui a linha atual do cursor.  
  
 **SQLSetPos** pode ser usado com qualquer instrução conjunto de resultados quando os atributos de cursor do identificador de instrução são definidos para usar cursores de servidor. As colunas do conjunto de resultados devem ser associadas para programar variáveis. Assim que o aplicativo busca uma linha, ele chama **SQLSetPos**(SQL_POSTION) para posicionar o cursor na linha. O aplicativo pode então chamar SQLSetPos(SQL_DELETE) para excluir a linha atual ou pode mover novos valores de dados para as variáveis do programa associado e chamar SQLSetPos(SQL_UPDATE) para atualizar a linha atual.  
  
 Aplicativos podem atualizar ou excluir qualquer linha no conjunto de linhas com **SQLSetPos**. Chamando **SQLSetPos** é uma alternativa conveniente para construir e executar uma instrução SQL. **SQLSetPos** opera no conjunto de linhas atual e pode ser usado somente após uma chamada para [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md).  
  
 Tamanho do conjunto de linhas é definido por uma chamada para [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) com um argumento de atributo de SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** usa um novo tamanho do conjunto de linhas, mas somente após uma chamada para **SQLFetch** ou **SQLFetchScroll**. Por exemplo, se o tamanho do conjunto de linhas é alterado, **SQLSetPos** é chamado e então **SQLFetch** ou **SQLFetchScroll** é chamado. A chamada para **SQLSetPos** usa o tamanho do conjunto de linhas antigo, mas **SQLFetch** ou **SQLFetchScroll** usa o novo tamanho do conjunto de linhas.  
  
 A primeira linha do conjunto de linhas é o número de linha 1. O argumento RowNumber **SQLSetPos** deve identificar uma linha no conjunto de linhas; ou seja, seu valor deve estar no intervalo entre 1 e o número de linhas buscado mais recentemente. Ele pode ser menor que o tamanho do conjunto de linhas. Se RowNumber for 0, a operação se aplicará a toda linha no conjunto de linhas.  
  
 A operação de exclusão de **SQLSetPos** faz com que a fonte de dados exclua uma ou mais linhas selecionadas de uma tabela. Para excluir linhas com **SQLSetPos**, o aplicativo chama **SQLSetPos** com Operation definido como SQL_DELETE e RowNumber definido como o número da linha para excluir. Se RowNumber for 0, todas as linhas do conjunto de linhas serão excluídas.  
  
 Após **SQLSetPos** retorna, a linha excluída será a linha atual e seu status será SQL_ROW_DELETED. A linha não pode ser usada em operações posicionadas adicionais, como chamadas a [SQLGetData](../native-client-odbc-api/sqlgetdata.md) ou **SQLSetPos**.  
  
 Quando você exclui todas as linhas do conjunto de linhas (RowNumber é igual a 0), o aplicativo pode impedir que o driver exclua determinadas linhas usando a matriz de operação de linha assim como para a operação de atualização do **SQLSetPos**.  
  
 Todas as linhas excluídas devem existir no conjunto de resultados. Se os buffers do aplicativo tiverem sido preenchidos pela busca e se uma matriz de status de linha tiver sido mantida, seus valores em cada uma das novas posições não deverão ser SQL_ROW_DELETED, SQL_ROW_ERROR ou SQL_ROW_NOROW.  
  
 Atualizações posicionadas também pode ser executadas usando a cláusula WHERE CURRENT OF nas instruções UPDATE, DELETE e INSERT. WHERE CURRENT OF requer um nome de cursor que o ODBC gerará quando o [SQLGetCursorName](../native-client-odbc-api/sqlgetcursorname.md) função é chamada, ou que você pode especificar chamando **SQLSetCursorName**. As etapas gerais a seguir são usadas para executar uma atualização WHERE CURRENT OF em um aplicativo ODBC:  
  
-   Chame **SQLSetCursorName** para estabelecer um nome de cursor para o identificador de instrução.  
  
-   Compile uma instrução SELECT com uma cláusula FOR UPDATE DE e execute-a.  
  
-   Chame **SQLFetchScroll** para recuperar um conjunto de linhas ou **SQLFetch** para recuperar uma linha.  
  
-   Chame **SQLSetPos** (SQL_POSITION) para posicionar o cursor na linha.  
  
-   Compilar e executar uma instrução UPDATE com uma cláusula WHERE CURRENT OF usando o nome de cursor definido com **SQLSetCursorName**.  
  
 Como alternativa, você poderia chamar **SQLGetCursorName** depois de executar a instrução SELECT em vez de chamar **SQLSetCursorName** antes de executar a instrução SELECT. **SQLGetCursorName** retorna um nome de cursor padrão atribuído por ODBC, se você não definir um nome de cursor usando **SQLSetCursorName**.  
  
 **SQLSetPos** é preferível a WHERE CURRENT OF quando você estiver usando cursores de servidor. Se você estiver usando um cursor atualizável estático com a biblioteca de cursores ODBC, a biblioteca de cursores implementará as atualizações WHERE CURRENT OF com os valores de chave para a tabela subjacente. Isso pode provocar atualizações não pretendidas, caso as chaves da tabela não foram exclusivas.  
  
## <a name="see-also"></a>Consulte também  
 [Uso de cursores &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
