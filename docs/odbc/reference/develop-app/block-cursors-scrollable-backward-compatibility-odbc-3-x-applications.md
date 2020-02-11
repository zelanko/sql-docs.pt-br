---
title: Compatibilidade de cursores de bloqueio e rolável para ODBC 3. x Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- SQLExtendedFetch function [ODBC], block cursors
- cursors [ODBC], compatibility issues
- SQLFetchScroll function [ODBC], block cursors
ms.assetid: 82f6cf68-cfde-4417-9788-d6382ca14bf8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d12906f8dec0bfb12fc861c067e6e615e758a3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68134985"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores para aplicativos 3.x ODBC
A existência de **SQLFetchScroll** e **SQLExtendedFetch** representa a primeira divisão clara em ODBC entre a API (interface de programação de aplicativo), que é o conjunto de funções que o aplicativo chama e a SPI (interface do provedor de serviços), que é o conjunto de funções que o Driver implementa. Essa divisão é necessária para balancear o requisito no ODBC *3. x*, que usa **SQLFetchScroll**, para se alinhar com os padrões e ser compatível com o ODBC *2. x*, que usa **SQLExtendedFetch**.  
  
 A API ODBC *3. x* , que é o conjunto de funções que o aplicativo chama, inclui **SQLFetchScroll** e atributos de instrução relacionados. O SPI ODBC *3. x* , que é o conjunto de funções que o Driver implementa, inclui **SQLFetchScroll**, **SQLExtendedFetch**e atributos de instrução relacionados. Como o ODBC não impõe formalmente essa divisão entre a API e o SPI, é possível que os aplicativos ODBC *3. x* chamem **SQLExtendedFetch** e atributos de instrução relacionados. No entanto, não há motivo para os aplicativos ODBC *3. x* fazer isso. Para obter mais informações sobre APIs e SPIs, consulte a introdução à [arquitetura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obter informações sobre como o Gerenciador de driver ODBC *3. x* mapeia chamadas para os drivers ODBC *2. x* e ODBC *3. x* e quais funções e atributos de instrução um driver ODBC *3. x* deve implementar para cursores de bloco e rolável, consulte [o que o driver faz](../../../odbc/reference/appendixes/what-the-driver-does.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.  
  
 A tabela a seguir resume quais funções e atributos de instrução um aplicativo ODBC *3. x* deve usar com cursores de bloqueio e rolável. Ele também lista as alterações entre ODBC *2. x* e ODBC *3. x* nessa área que os aplicativos ODBC *3. x* devem estar cientes para serem compatíveis com os drivers ODBC *2. x* .  
  
|Função ou<br /><br /> atributo de instrução|Comentários|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Aponta para o indicador a ser usado com **SQLFetchScroll**.<br /><br /> Quando um aplicativo define isso em um driver ODBC *2. x* , ele deve apontar para um indicador de comprimento fixo.|  
|SQL_ATTR_ROW_STATUS_PTR|Aponta para a matriz de status de linha preenchida por **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**e **SQLSetPos**.<br /><br /> Se um aplicativo definir isso em um driver ODBC *2. x* e chamar **SQLBulkOperation** com uma *operação* de SQL_ADD antes de chamar **SQLFetchScroll**, **SQLFetch**ou **SQLExtendedFetch**, SQLSTATE hy011 (o atributo não pode ser definido agora) será retornado.<br /><br /> Quando um aplicativo chama **SQLFetch** em um driver ODBC *2. x* , **SQLFetch** é mapeado para **SQLExtendedFetch** e, portanto, retorna valores nessa matriz.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Aponta para o buffer no qual **SQLFetch** e **SQLFetchScroll** retornam o número de linhas buscadas.<br /><br /> Quando um aplicativo chama **SQLFetch** em um driver ODBC *2. x* , **SQLFetch** é mapeado para **SQLExtendedFetch** e, portanto, retorna um valor nesse buffer.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Define o tamanho do conjunto de linhas.<br /><br /> Se um aplicativo chamar **SQLBulkOperations** com uma *operação* de SQL_ADD em um driver ODBC *2. x* , SQL_ROWSET_SIZE será usado para a chamada, não SQL_ATTR_ROW_ARRAY_SIZE, porque a chamada é mapeada para **SQLSetPos** com uma *operação* de SQL_ADD, que usa SQL_ROWSET_SIZE.<br /><br /> Chamar **SQLSetPos** com uma *operação* de SQL_ADD ou **SQLExtendedFetch** em um driver ODBC *2. x* usa SQL_ROWSET_SIZE.<br /><br /> Chamar **SQLFetch** ou **SQLFetchScroll** em um driver ODBC *2. x* usa SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLBulkOperations**|Executa operações de inserção e de indicador. Quando **SQLBulkOperations** com uma *operação* de SQL_ADD é chamado em um driver ODBC *2. x* , ele é mapeado para **SQLSetPos** com uma *operação* de SQL_ADD. Veja a seguir os detalhes de implementação:<br /><br /> -Ao trabalhar com um driver ODBC *2. x* , um aplicativo deve usar apenas o ARD atribuído implicitamente associado ao *StatementHandle*; Ele não pode alocar outro ARD para adicionar linhas, porque não há suporte para operações de descritor explícitas em um driver ODBC *2. x* . Um aplicativo deve usar **SQLBindCol** para associar ao ARD, não **SQLSetDescField** ou **SQLSetDescRec**.<br />-Ao chamar um driver ODBC *3. x* , um aplicativo pode chamar **SQLBulkOperations** com uma *operação* de SQL_ADD antes de chamar **SQLFetch** ou **SQLFetchScroll**. Ao chamar um driver ODBC *2. x* , um aplicativo deve chamar **SQLFetchScroll** antes de chamar **SQLBulkOperations** com uma operação de SQL_ADD.|  
|**SQLFetch**|Retorna o próximo conjunto de linhas. Veja a seguir os detalhes de implementação:<br /><br /> -Quando um aplicativo chama **SQLFetch** em um driver ODBC *2. x* , ele é mapeado para **SQLExtendedFetch**.<br />-Quando um aplicativo chama **SQLFetch** em um driver ODBC *3. x* , ele retorna o número de linhas especificado com o atributo instrução SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLFetchScroll**|Retorna o conjunto de linhas especificado. Veja a seguir os detalhes de implementação:<br /><br /> -Quando um aplicativo chama **SQLFetchScroll** em um driver ODBC *2. x* , ele retorna SQLSTATE 01S01 (erro na linha) antes de cada erro que se aplica a uma única linha. Ele faz isso somente porque o Gerenciador de driver ODBC *3. x* mapeia isso para **SQLExtendedFetch** e **SQLExtendedFetch** retorna este SQLSTATE. Quando um aplicativo chama **SQLFetchScroll** em um driver ODBC *3. x* , ele nunca retorna SQLSTATE 01S01 (erro na linha).<br />-Quando um aplicativo chama **SQLFetchScroll** em um driver ODBC *2. x* com *FetchOrientation* definido como SQL_FETCH_BOOKMARK, o argumento *FetchOffset* deve ser definido como 0. SQLSTATE HYC00 (recurso opcional não implementado) será retornado se a busca de indicador com base em deslocamento for tentada com um driver ODBC *2. x* .|  
  
> [!NOTE]  
>  Os aplicativos ODBC *3. x* não devem usar **SQLExtendedFetch** ou o atributo de instrução SQL_ROWSET_SIZE. Em vez disso, eles devem usar **SQLFetchScroll** e o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE. Os aplicativos ODBC *3. x* não devem usar **SQLSetPos** com uma *operação* de SQL_ADD, mas devem usar **SQLBulkOperations** com uma *operação* de SQL_ADD.
