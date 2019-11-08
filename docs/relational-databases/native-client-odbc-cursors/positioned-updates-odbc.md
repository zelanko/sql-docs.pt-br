---
title: Atualizações posicionadas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1424d4e7ff08cee6dea1e53dfac0e5cf231ea266
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784392"
---
# <a name="positioned-updates-odbc"></a>Atualizações posicionadas (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

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
  
 **SQLSetPos** pode ser usado com qualquer conjunto de resultados de instrução quando a instrução manipula atributos de cursor está definida para usar cursores de servidor. As colunas do conjunto de resultados devem ser associadas para programar variáveis. Assim que o aplicativo tiver obtido uma linha, ele chamará **SQLSetPos**(SQL_POSTION) para posicionar o cursor na linha. O aplicativo pode então chamar SQLSetPos(SQL_DELETE) para excluir a linha atual ou pode mover novos valores de dados para as variáveis do programa associado e chamar SQLSetPos(SQL_UPDATE) para atualizar a linha atual.  
  
 Os aplicativos podem atualizar ou excluir qualquer linha no conjunto de linhas com **SQLSetPos**. Chamar **SQLSetPos** é uma alternativa conveniente para construir e executar uma instrução SQL. **SQLSetPos** opera no conjunto de linhas atual e pode ser usado somente após uma chamada para [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md).  
  
 O tamanho do conjunto de linhas é definido por uma chamada para [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) com um argumento de atributo de SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** usa um novo tamanho de conjunto de linhas, mas somente após uma chamada para **SQLFetch** ou **SQLFetchScroll**. Por exemplo, se o tamanho do conjunto de linhas for alterado, **SQLSetPos** será chamado e, em seguida, **SQLFetch** ou **SQLFetchScroll** será chamado. A chamada para **SQLSetPos** usa o tamanho antigo do conjunto de linhas, mas **SQLFetch** ou **SQLFetchScroll** usa o novo tamanho do conjunto de linhas.  
  
 A primeira linha do conjunto de linhas é o número de linha 1. O argumento RowNumber em **SQLSetPos** deve identificar uma linha no conjunto de linhas; ou seja, seu valor deve estar no intervalo entre 1 e o número de linhas que foram buscadas mais recentemente. Ele pode ser menor que o tamanho do conjunto de linhas. Se RowNumber for 0, a operação se aplicará a toda linha no conjunto de linhas.  
  
 A operação de exclusão de **SQLSetPos** faz com que a fonte de dados exclua uma ou mais linhas selecionadas de uma tabela. Para excluir linhas com **SQLSetPos**, o aplicativo chama **SQLSetPos** com a operação definida como SQL_DELETE e RowNumber definido como o número da linha a ser excluída. Se RowNumber for 0, todas as linhas do conjunto de linhas serão excluídas.  
  
 Depois que **SQLSetPos** retorna, a linha excluída é a linha atual e seu status é SQL_ROW_DELETED. A linha não pode ser usada em nenhuma operação posicionada adicional, como chamadas para [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) ou **SQLSetPos**.  
  
 Quando você exclui todas as linhas do conjunto de linhas (RowNumber é igual a 0), o aplicativo pode impedir que o driver exclua determinadas linhas usando a matriz de operação de linha, assim como para a operação de atualização de **SQLSetPos**.  
  
 Todas as linhas excluídas devem existir no conjunto de resultados. Se os buffers do aplicativo tiverem sido preenchidos pela busca e se uma matriz de status de linha tiver sido mantida, seus valores em cada uma das novas posições não deverão ser SQL_ROW_DELETED, SQL_ROW_ERROR ou SQL_ROW_NOROW.  
  
 Atualizações posicionadas também pode ser executadas usando a cláusula WHERE CURRENT OF nas instruções UPDATE, DELETE e INSERT. ONDE CURRENT OF exige um nome de cursor que o ODBC gerará quando a função [SQLGetCursorName](../../relational-databases/native-client-odbc-api/sqlgetcursorname.md) for chamada ou que você pode especificar chamando **SQLSetCursorName**. As etapas gerais a seguir são usadas para executar uma atualização WHERE CURRENT OF em um aplicativo ODBC:  
  
-   Chame **SQLSetCursorName** para estabelecer um nome de cursor para o identificador de instrução.  
  
-   Compile uma instrução SELECT com uma cláusula FOR UPDATE DE e execute-a.  
  
-   Chame **SQLFetchScroll** para recuperar um conjunto de linhas ou **SQLFetch** para recuperar uma linha.  
  
-   Chame **SQLSetPos** (SQL_POSITION) para posicionar o cursor na linha.  
  
-   Crie e execute uma instrução UPDATE com uma cláusula WHERE CURRENT OF usando o nome do cursor definido com **SQLSetCursorName**.  
  
 Como alternativa, você poderia chamar **SQLGetCursorName** depois de executar a instrução SELECT em vez de chamar **SQLSetCursorName** antes de executar a instrução SELECT. **SQLGetCursorName** retorna um nome de cursor padrão atribuído pelo ODBC se você não definir um nome de cursor usando **SQLSetCursorName**.  
  
 **SQLSetPos** é preferível quando atual de quando você está usando cursores de servidor. Se você estiver usando um cursor atualizável estático com a biblioteca de cursores ODBC, a biblioteca de cursores implementará as atualizações WHERE CURRENT OF com os valores de chave para a tabela subjacente. Isso pode provocar atualizações não pretendidas, caso as chaves da tabela não foram exclusivas.  
  
## <a name="see-also"></a>Consulte também  
 [Usando cursores &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
