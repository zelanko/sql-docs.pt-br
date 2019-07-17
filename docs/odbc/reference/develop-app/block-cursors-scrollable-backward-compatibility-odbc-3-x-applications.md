---
title: Bloco e compatibilidade de cursores roláveis para ODBC 3. x | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134985"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores para aplicativos 3.x ODBC
A existência de ambos **SQLFetchScroll** e **SQLExtendedFetch** representa o limpar primeiro dividido entre o aplicativo de Interface de programação (API), que é o conjunto de funções ODBC a chamadas do aplicativo e o Service Provider Interface (SPI), que é o conjunto de funções implementa o driver. Essa divisão é necessário para equilibrar o requisito de ODBC *3.x*, que usa **SQLFetchScroll**, para alinhar com os padrões e ser compatível com ODBC *2.x*, que usa **SQLExtendedFetch**.  
  
 O ODBC *3.x* API, que é o conjunto de funções o aplicativo chama, inclui **SQLFetchScroll** e relacionados a atributos de instrução. O ODBC *3.x* SPI, que é o conjunto de funções o driver implementa, inclui **SQLFetchScroll**, **SQLExtendedFetch**e relacionados a atributos de instrução. Como o ODBC não impõe formalmente essa divisão entre a API e o SPI, é possível para ODBC *3.x* aplicativos chamem **SQLExtendedFetch** e relacionados a atributos de instrução. No entanto, não há nenhum motivo para ODBC *3.x* aplicativos para fazer isso. Para obter mais informações sobre as APIs e SPIs, consulte a introdução [arquitetura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obter informações sobre como o ODBC *3.x* Gerenciador de Driver mapeia chamadas ODBC *2.x* e ODBC *3.x* drivers e quais funções e a instrução atributos ODBC *3.x* driver deve implementar para cursores roláveis e de bloco, consulte [o que o Driver faz](../../../odbc/reference/appendixes/what-the-driver-does.md) no Apêndice g: Diretrizes de driver para compatibilidade com versões anteriores.  
  
 A tabela a seguir resume quais funções e atributos de instrução ODBC *3.x* aplicativo deve usar com o bloco e cursores roláveis. Ela também lista as alterações entre o ODBC *2.x* e ODBC *3.x* nessa área que o ODBC *3.x* aplicativos devem estar atento ser compatível com ODBC *2.x* drivers.  
  
|Função ou<br /><br /> atributo de instrução|Comentários|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Aponta para o indicador a ser usado com **SQLFetchScroll**.<br /><br /> Quando um aplicativo define isso em um ODBC *2.x* driver, isso deve apontar para um indicador de comprimento fixo.|  
|SQL_ATTR_ROW_STATUS_PTR|Aponta para a matriz de status de linha é preenchido por **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, e **SQLSetPos**.<br /><br /> Se um aplicativo define isso em um ODBC *2.x* driver e chama **SQLBulkOperation** com um *operação* de SQL_ADD antes de chamar **SQLFetchScroll**, **SQLFetch**, ou **SQLExtendedFetch**, SQLSTATE HY011 (atributo não pode ser definido agora) é retornado.<br /><br /> Quando um aplicativo chama **SQLFetch** em um ODBC *2.x* driver **SQLFetch** é mapeado para **SQLExtendedFetch** e, portanto, retorna valores nessa matriz.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Aponta para o buffer no qual **SQLFetch** e **SQLFetchScroll** retornar o número de linhas buscadas.<br /><br /> Quando um aplicativo chama **SQLFetch** em um ODBC *2.x* driver **SQLFetch** é mapeado para **SQLExtendedFetch** e, portanto, retorna um valor nesse buffer.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Define o tamanho do conjunto de linhas.<br /><br /> Se um aplicativo chamar **SQLBulkOperations** com um *operação* de SQL_ADD no ODBC *2.x* driver, SQL_ROWSET_SIZE será usado para a chamada, não SQL_ATTR_ROW_ARRAY_ O tamanho, porque a chamada está mapeada para **SQLSetPos** com um *operação* de SQL_ADD, que usa SQL_ROWSET_SIZE.<br /><br /> Chamando **SQLSetPos** com um *operação* de SQL_ADD ou **SQLExtendedFetch** em um ODBC *2.x* SQL_ROWSET_SIZE usa o driver.<br /><br /> Chamando **SQLFetch** ou **SQLFetchScroll** em um ODBC *2.x* driver usa SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLBulkOperations**|Executa operações de inserção e indicador. Quando **SQLBulkOperations** com um *operação* de SQL_ADD é chamado em um ODBC *2.x* driver, ele é mapeado para **SQLSetPos** com um  *Operação* de SQL_ADD. A seguir estão os detalhes de implementação:<br /><br /> -Ao trabalhar com ODBC *2.x* driver, um aplicativo deve usar somente a descartar implicitamente alocado associado com o *StatementHandle*; ele não é possível alocar outro descartar para adicionar linhas, porque explícita Não há suporte para operações de descritor ODBC *2.x* driver. Um aplicativo deve usar **SQLBindCol** para associar ao descartar, não **SQLSetDescField** ou **SQLSetDescRec**.<br />-Ao chamar um ODBC *3.x* driver, um aplicativo pode chamar **SQLBulkOperations** com um *operação* de SQL_ADD antes de chamar **SQLFetch**ou **SQLFetchScroll**. Ao chamar um ODBC *2.x* driver, um aplicativo deve chamar **SQLFetchScroll** antes de chamar **SQLBulkOperations** com uma operação de SQL_ADD.|  
|**SQLFetch**|Retorna o próximo conjunto de linhas. A seguir estão os detalhes de implementação:<br /><br /> -Quando um aplicativo chama **SQLFetch** em um ODBC *2.x* driver, ele é mapeado para **SQLExtendedFetch**.<br />-Quando um aplicativo chama **SQLFetch** em um ODBC *3.x* driver, ele retorna o número de linhas especificado com o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLFetchScroll**|Retorna o conjunto de linhas especificado. A seguir estão os detalhes de implementação:<br /><br /> -Quando um aplicativo chama **SQLFetchScroll** em um ODBC *2.x* driver, ele retornará SQLSTATE 01S01 (erro na linha) antes de cada erro que se aplica a uma única linha. Ele faz isso, apenas porque o ODBC *3.x* Gerenciador de Driver é mapeado para **SQLExtendedFetch** e **SQLExtendedFetch** retorna esse SQLSTATE. Quando um aplicativo chama **SQLFetchScroll** em um ODBC *3.x* driver, ele nunca retornará SQLSTATE 01S01 (erro na linha).<br />-Quando um aplicativo chama **SQLFetchScroll** em um ODBC *2.x* driver com *FetchOrientation* definido como SQL_FETCH_BOOKMARK, o *FetchOffset* argumento deve ser definido como 0. SQLSTATE HYC00 (recurso opcional não implementado) será retornado se o indicador com base no deslocamento de busca é tentada com ODBC *2.x* driver.|  
  
> [!NOTE]  
>  ODBC *3.x* aplicativos não devem usar **SQLExtendedFetch** ou o atributo da instrução SQL_ROWSET_SIZE. Em vez disso, eles devem usar **SQLFetchScroll** e o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE. ODBC *3.x* aplicativos não devem usar **SQLSetPos** com um *operação* de SQL_ADD, mas deve usar **SQLBulkOperations** com um  *Operação* de SQL_ADD.
