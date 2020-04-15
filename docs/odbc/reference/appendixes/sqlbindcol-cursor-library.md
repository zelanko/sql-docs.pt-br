---
title: SQLBindCol (Biblioteca Cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c29909a96f147a0f5ebc2140a68072dfe544255
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305467"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLBindCol** na biblioteca do cursor. Para obter informações gerais sobre **o SQLBindCol,** consulte [SQLBindCol Function](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
 Um aplicativo aloca um ou mais buffers para a biblioteca do cursor para retornar o conjunto de linhas atual. Ele chama **SQLBindCol** uma ou mais vezes para vincular esses buffers ao conjunto de resultados.  
  
 Um aplicativo pode chamar **o SQLBindCol** para revincular colunas de conjunto de resultados depois de ter chamado **SQLExtendedFetch,** **SQLFetch**ou **SQLFetchScroll,** desde que o tipo de dados C, o tamanho da coluna e os dígitos decimais da coluna vinculada permaneçam os mesmos. O aplicativo não precisa fechar o cursor para revincular colunas a diferentes endereços.  
  
 A biblioteca do cursor suporta a definição do atributo de declaração SQL_ATTR_ROW_BIND_OFFSET_PTR para usar deslocamentos de vinculação. **(SQLBindCol** não precisa ser chamado para que essa revinculação ocorra.) Se a biblioteca do cursor for usada com um driver ODBC *3.x,* o deslocamento de vinculação não será usado quando **o SQLFetch** for chamado. O deslocamento de vinculação é usado se **o SQLFetch** for chamado quando a biblioteca do cursor for usada com um driver ODBC *2.x* porque **o SQLFetch** é então mapeado para **SQLExtendedFetch**.  
  
 A biblioteca do cursor suporta chamar **SQLBindCol** para vincular a coluna marcador.  
  
 Ao trabalhar com um driver ODBC *2.x,* a biblioteca do cursor retorna SQLSTATE HY090 (comprimento inválido de string ou buffer) quando **o SQLBindCol** é chamado para definir o comprimento do buffer para uma coluna de marcação de guia para um valor não igual a 4. Ao trabalhar com um driver ODBC *3.x,* a biblioteca do cursor permite que o buffer seja de qualquer tamanho.
