---
title: Usando cursores de bloco | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306787"
---
# <a name="using-block-cursors"></a>Usar cursores em bloco
O suporte para cursores de bloco é incorporado ao ODBC 3. *x*. **SQLFetch** pode ser usado somente para buscas de LinhaMúltipla quando chamado no ODBC 3. *x*; se um ODBC 2. *x* Application chama **SQLFetch**, ele abrirá apenas um cursor de linha única e somente avanço. Quando um ODBC 3. *x* aplicativo chama **SQLFetch** em um ODBC 2. *x* , ele retorna uma única linha, a menos que o driver dê suporte a **SQLExtendedFetch**. Para obter mais informações, consulte [cursores de bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.  
  
 Para usar cursores de bloco, o aplicativo define o tamanho do conjunto de linhas, associa os buffers de conjunto de linhas (conforme descrito na seção anterior), opcionalmente, define os atributos de instrução SQL_ATTR_ROWS_FETCHED_PTR e SQL_ATTR_ROW_STATUS_PTR e chama **SQLFetch** ou **SQLFetchScroll** para buscar um bloco de linhas. O aplicativo pode alterar o tamanho do conjunto de linhas e associar novos buffers de conjunto de linhas (chamando **SQLBindCol** ou especificando um deslocamento de ligação) mesmo depois que as linhas tiverem sido buscadas.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tamanho do conjunto de linhas](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [Número de linhas buscadas e status](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData e cursores de bloco; bloco em curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
