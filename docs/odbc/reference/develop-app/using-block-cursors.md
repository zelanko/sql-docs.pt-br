---
title: Usando cursores em bloco | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 388995cd5cb8a711d72533685c14088a7e908475
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313511"
---
# <a name="using-block-cursors"></a>Usar cursores em bloco
Suporte para cursores em bloco é incorporado ao ODBC 3. *x*. **SQLFetch** pode ser usado apenas para buscas de várias linhas quando chamado em ODBC 3. *x*; se o ODBC 2. *x* aplicativo chamará **SQLFetch**, ele será aberto somente um cursor de uma única linha, apenas de encaminhamento. Quando um ODBC 3. *x* aplicativo chamará **SQLFetch** em um ODBC 2. *x* driver, ele retorna uma única linha, a menos que o driver suporta **SQLExtendedFetch**. Para obter mais informações, consulte [cursores em bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no Apêndice g: Diretrizes de driver para compatibilidade com versões anteriores.  
  
 Para usar cursores em bloco, o aplicativo define o tamanho do conjunto de linhas, associa a buffers de conjunto de linhas (conforme descrito na seção anterior), opcionalmente, define os atributos de instrução SQL_ATTR_ROWS_FETCHED_PTR e SQL_ATTR_ROW_STATUS_PTR e chamadas **SQLFetch**  ou **SQLFetchScroll** para buscar um bloco de linhas. O aplicativo pode alterar o tamanho do conjunto de linhas e vincular novos buffers rowset (chamando **SQLBindCol** ou especificando um deslocamento de bind), mesmo depois de linhas foram buscadas.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tamanho do conjunto de linhas](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [Número de linhas buscadas e status](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData e cursores em bloco; curso de bloco](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
