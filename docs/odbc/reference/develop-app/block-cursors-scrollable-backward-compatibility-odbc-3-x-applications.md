---
title: Compatibilidade de cursores de blocos e roláveis para ODBC 3.x | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c526eff6e19014c923f05ad91551a7d7c66f5294
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306337"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores para aplicativos 3.x ODBC
A existência tanto do **SQLFetchScroll** quanto **do SQLExtendedFetch** representa a primeira divisão clara no ODBC entre a API (Application Programming Interface, interface de programação de aplicativos), que é o conjunto de funções que as chamadas de aplicativos e a Interface do Provedor de Serviços (SPI), que é o conjunto de funções que o driver implementa. Esta divisão é necessária para equilibrar a exigência no ODBC *3.x*, que usa **SQLFetchScroll,** para se alinhar com os padrões e ser compatível com o ODBC *2.x*, que usa **SQLExtendedFetch**.  
  
 A API ODBC *3.x,* que é o conjunto de funções que as chamadas do aplicativo chamam, inclui **SQLFetchScroll** e atributos de declaração relacionados. O ODBC *3.x* SPI, que é o conjunto de funções que o driver implementa, inclui **SQLFetchScroll,** **SQLExtendedFetch**e atributos de declaração relacionados. Como o ODBC não aplica formalmente essa divisão entre a API e o SPI, é possível que os aplicativos ODBC *3.x* chamem **sqlExtendedFetch** e atributos de declaração relacionados. No entanto, não há razão para que as aplicações ODBC *3.x* façam isso. Para obter mais informações sobre APIs e SPIs, consulte a introdução da [Arquitetura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obter informações sobre como o ODBC *3.x* Driver Manager mapeia chamadas para drivers ODBC *2.x* e ODBC *3.x,* e quais funções e atributos de declaração um driver ODBC *3.x* deve implementar para cursores de bloco e roláveis, consulte o que o driver faz no [apêndice](../../../odbc/reference/appendixes/what-the-driver-does.md) G: Diretrizes do driver para compatibilidade retrógrada.  
  
 A tabela a seguir resume quais funções e atributos de declaração um aplicativo ODBC *3.x* deve ser usado com cursores de bloco e roláveis. Ele também lista alterações entre o ODBC *2.x* e o ODBC *3.x* nesta área que os aplicativos ODBC *3.x* devem estar cientes de serem compatíveis com drivers ODBC *2.x.*  
  
|Função ou<br /><br /> atributo de instrução|Comentários|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Aponta para o marcador a ser usado com **SQLFetchScroll**.<br /><br /> Quando um aplicativo define isso em um driver ODBC *2.x,* isso deve apontar para um marcador de comprimento fixo.|  
|SQL_ATTR_ROW_STATUS_PTR|Aponta para o array de status de linha preenchido por **SQLFetch,** **SQLFetchScroll,** **SQLBulkOperations**e **SQLSetPos**.<br /><br /> Se um aplicativo definir isso em um driver ODBC *2.x* e chamar **SQLBulkOperation** com uma *operação* de SQL_ADD antes de chamar **SQLFetchScroll,** **SQLFetch**ou **SQLExtendedFetch**, SQLSTATE HY011 (Atributo não pode ser definido agora) é devolvido.<br /><br /> Quando um aplicativo chama **sqlfetch** em um driver ODBC *2.x,* **sQLFetch** é mapeado para **SQLExtendedFetch** e, portanto, retorna valores nesta matriz.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Aponta para o buffer no qual **SQLFetch** e **SQLFetchScroll** retornam o número de linhas buscadas.<br /><br /> Quando um aplicativo chama **sqlfetch** em um driver ODBC *2.x,* **SQLFetch** é mapeado para **SQLExtendedFetch** e, portanto, retorna um valor neste buffer.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Define o tamanho do conjunto de linhas.<br /><br /> Se um aplicativo chamar **SQLBulkOperations** com uma *operação* de SQL_ADD em um driver ODBC *2.x,* SQL_ROWSET_SIZE será usado para a chamada, não SQL_ATTR_ROW_ARRAY_SIZE, porque a chamada é mapeada para **SQLSetPos** com uma *Operação* de SQL_ADD, que usa SQL_ROWSET_SIZE.<br /><br /> Chamar **SQLSetPos** com uma *operação* de SQL_ADD ou **SQLExtendedFetch** em um driver ODBC *2.x* usa SQL_ROWSET_SIZE.<br /><br /> Chamar **SQLFetch** ou **SQLFetchScroll** em um driver ODBC *2.x* usa SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLBulkOperations**|Realiza operações de inserção e marcação. Quando **o SQLBulkOperations** com uma *Operação* de SQL_ADD é chamado de driver ODBC *2.x,* ele é mapeado para **SQLSetPos** com uma *Operação* de SQL_ADD. A seguir, os detalhes da implementação:<br /><br /> - Ao trabalhar com um driver ODBC *2.x,* um aplicativo deve usar apenas o ARD implicitamente alocado associado ao *StatementHandle;* ele não pode alocar outro ARD para adicionar linhas, porque as operações explícitas de descritores não são suportadas em um driver ODBC *2.x.* Um aplicativo deve usar **o SQLBindCol** para se ligar ao ARD, não ao **SQLSetDescField** ou **ao SQLSetDescRec**.<br />- Ao ligar para um driver ODBC *3.x,* um aplicativo pode ligar para **SQLBulkOperations** com uma *operação* de SQL_ADD antes de ligar para **SQLFetch** ou **SQLFetchScroll**. Ao ligar para um driver ODBC *2.x,* um aplicativo deve ligar para **o SQLFetchScroll** antes de ligar para **a SQLBulkOperations** com uma operação de SQL_ADD.|  
|**SQLFetch**|Retorna o próximo conjunto de linhas. A seguir, os detalhes da implementação:<br /><br /> - Quando um aplicativo chama **sqlfetch** em um driver ODBC *2.x,* ele é mapeado para **SQLExtendedFetch**.<br />- Quando um aplicativo chama **sqlfetch** em um driver ODBC *3.x,* ele retorna o número de linhas especificadas com o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLFetchScroll**|Retorna o conjunto de linhas especificado. A seguir, os detalhes da implementação:<br /><br /> - Quando um aplicativo chama **SQLFetchScroll** em um driver ODBC *2.x,* ele retorna SQLSTATE 01S01 (Erro em linha) antes de cada erro que se aplica a uma única linha. Ele faz isso apenas porque o Gerenciador de Driver ODBC *3.x* mapeia isso para **SQLExtendedFetch** e **SQLExtendedFetch** retorna este SQLSTATE. Quando um aplicativo chama **SQLFetchScroll** em um driver ODBC *3.x,* ele nunca retorna SQLSTATE 01S01 (Erro em linha).<br />- Quando um aplicativo chama **SQLFetchScroll** em um driver ODBC *2.x* com *FetchOrientation* definido para SQL_FETCH_BOOKMARK, o argumento *FetchOffset* deve ser definido como 0. SQLSTATE HYC00 (recurso opcional não implementado) é devolvido se a busca de marcadores baseada em deslocamento for tentada com um driver ODBC *2.x.*|  
  
> [!NOTE]  
>  Os aplicativos ODBC *3.x* não devem usar **sqlextendedfetch** ou o atributo de declaração SQL_ROWSET_SIZE. Em vez disso, eles devem usar **SQLFetchScroll** e o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE. Os aplicativos ODBC *3.x* não devem usar **SQLSetPos** com uma *operação* de SQL_ADD, mas devem usar **SQLBulkOperations** com uma *operação* de SQL_ADD.
