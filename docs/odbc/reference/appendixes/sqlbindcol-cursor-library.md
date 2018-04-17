---
title: SQLBindCol (biblioteca de Cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eeca90b8de3ce65e8da68d6aabac89b2181ed047
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLBindCol** função na biblioteca de cursor. Para obter informações gerais sobre **SQLBindCol**, consulte [função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
 Um aplicativo aloca um ou mais buffers para a biblioteca de cursor retornar o conjunto de linhas atual no. Ele chama **SQLBindCol** uma ou mais vezes para associar esses buffers para o conjunto de resultados.  
  
 Um aplicativo pode chamar **SQLBindCol** para reassociar resultado conjunto de colunas depois que ela é chamada de **SQLExtendedFetch**, **SQLFetch**, ou **SQLFetchScroll**, contanto que o tipo de dados C, tamanho da coluna e casas decimais da coluna associada permanecem os mesmos. O aplicativo não precisa fechar o cursor para reassociar colunas para endereços diferentes.  
  
 A biblioteca de cursores dá suporte à configuração do atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR para usar os deslocamentos de ligação. (**SQLBindCol** não precisa ser chamado para essa nova associação ocorra.) Se a biblioteca de cursores é usada com um ODBC 3*. x* driver, o deslocamento de ligação não é usado quando **SQLFetch** é chamado. O deslocamento de ligação é usado se **SQLFetch** é chamado quando a biblioteca de cursores é usada com um ODBC 2. *x* driver porque **SQLFetch** , em seguida, é mapeado para **SQLExtendedFetch**.  
  
 A biblioteca de cursores dá suporte à chamada **SQLBindCol** para associar a coluna de indicador.  
  
 Ao trabalhar com um ODBC 2. *x* driver, a biblioteca de cursores retornará SQLSTATE HY090 (comprimento inválido de buffer ou cadeia de caracteres) quando **SQLBindCol** é chamado para definir o tamanho do buffer para uma coluna de indicador para um valor não é igual a 4. Ao trabalhar com um ODBC 3*. x* driver, a biblioteca de cursores permite que o buffer qualquer tamanho.
