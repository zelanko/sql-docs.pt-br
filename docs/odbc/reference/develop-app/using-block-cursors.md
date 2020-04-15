---
title: Usando cursors de bloco | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f5c487bd8b60a83c709399cb9673dc0b015bd79d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306787"
---
# <a name="using-block-cursors"></a>Usar cursores em bloco
O suporte para cursores de bloco é incorporado no ODBC 3. *x*. **SQLFetch** só pode ser usado para buscas multi-row quando chamado em ODBC 3. *x*; se um ODBC 2. *x* chamadas de aplicativo **SQLFetch,** ele abrirá apenas um cursor de linha única, somente para a frente. Quando um ODBC 3. *x* aplicativo chama **SQLFetch** em um ODBC 2. *x* driver, ele retorna uma única linha a menos que o driver suporte **SQLExtendedFetch**. Para obter mais informações, consulte [Cursors de bloco, cursores roláveis e compatibilidade retrógrada](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no apêndice G: Diretrizes do driver para compatibilidade retrógrada.  
  
 Para usar cursores de bloco, o aplicativo define o tamanho do conjunto de linhas, liga os buffers de conjunto de linhas (conforme descrito na seção anterior), define opcionalmente os atributos de declaração SQL_ATTR_ROWS_FETCHED_PTR e SQL_ATTR_ROW_STATUS_PTR e chama **SQLFetch** ou **SQLFetchScroll** para buscar um bloco de linhas. O aplicativo pode alterar o tamanho do conjunto de linhas e vincular novos buffers de conjunto de linhas (ligando para **SQLBindCol** ou especificando um deslocamento de vinculação) mesmo depois que as linhas forem buscadas.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tamanho do conjunto de linhas](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [Número de linhas buscadas e status](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData e Cursors de bloco; bloco curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
