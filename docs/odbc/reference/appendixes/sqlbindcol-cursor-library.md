---
title: SQLBindCol (biblioteca de cursores) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71afc3c0bac0ea64285c450640d96fe5f5d709b0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064970"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLBindCol** função na biblioteca de cursor. Para obter informações gerais sobre **SQLBindCol**, consulte [função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
 Um aplicativo aloca um ou mais buffers para a biblioteca de cursor retornar o conjunto de linhas atual no. Ele chama **SQLBindCol** uma ou mais vezes para associar esses buffers para o conjunto de resultados.  
  
 Um aplicativo pode chamar **SQLBindCol** associar novamente o resultado, definir colunas depois que ele é chamado **SQLExtendedFetch**, **SQLFetch**, ou **SQLFetchScroll**, desde que o tipo de dados C, tamanho da coluna e dígitos decimais da coluna acoplada permanecem os mesmos. O aplicativo não precisa fechar o cursor para reassociar colunas para endereços diferentes.  
  
 A biblioteca de cursores dá suporte à configuração do atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR para usar os deslocamentos de associação. (**SQLBindCol** não precisa ser chamado para essa nova associação ocorra.) Se a biblioteca de cursores é usada com ODBC *3.x* driver, o deslocamento de associação não é usado quando **SQLFetch** é chamado. O deslocamento de ligação é usado se **SQLFetch** é chamado quando a biblioteca de cursores é usada com ODBC *2.x* driver porque **SQLFetch** , em seguida, é mapeado para  **SQLExtendedFetch**.  
  
 A biblioteca de cursores dá suporte a chamar **SQLBindCol** para associar a coluna de indicador.  
  
 Ao trabalhar com ODBC *2.x* driver, a biblioteca de cursores retornará SQLSTATE HY090 (comprimento inválido de buffer ou cadeia de caracteres) quando **SQLBindCol** é chamado para definir o comprimento do buffer para uma coluna de indicador a um valor não igual a 4. Ao trabalhar com ODBC *3.x* driver, a biblioteca de cursores permite que o buffer para ser de qualquer tamanho.
