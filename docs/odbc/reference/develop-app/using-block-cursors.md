---
title: Usando cursores em bloco | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 51f02b5b243286a650897fecdcac5d8778bd3f40
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-block-cursors"></a>Usando cursores em bloco
Suporte para cursores em bloco é criado em ODBC 3. *x*. **SQLFetch** pode ser usado apenas para buscas multilinha quando chamado em ODBC 3.* x*; se o ODBC 2.* x* aplicativo chama **SQLFetch**, ele será aberto apenas um cursor de única linha, somente encaminhamento. Quando um ODBC 3. *x* aplicativo chama **SQLFetch** em um ODBC 2.* x* driver, ele retorna uma única linha, a menos que o driver dá suporte a **SQLExtendedFetch**. Para obter mais informações, consulte [cursores em bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.  
  
 Para usar cursores em bloco, o aplicativo define o tamanho do conjunto de linhas, e associa o conjunto de linhas buffers (conforme descrito na seção anterior), opcionalmente, define os atributos de instrução SQL_ATTR_ROWS_FETCHED_PTR e SQL_ATTR_ROW_STATUS_PTR e chamadas **SQLFetch ** ou **SQLFetchScroll** para buscar um bloco de linhas. O aplicativo pode alterar o tamanho do conjunto de linhas e associar os buffers do novo conjunto de linhas (chamando **SQLBindCol** ou especificando um deslocamento de ligação) mesmo depois que linhas foram buscadas.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tamanho do conjunto de linhas](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [Número de linhas buscadas e status](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData e cursores em bloco; curso de bloco](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
