---
description: Rolar e buscar linhas (ODBC)
title: Rolagem e busca de linhas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6fcdd2cd635a7da66a5d81c4beb24088f96382b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476488"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>Rolar e buscar linhas (ODBC)
Ao usar um cursor rolável, os aplicativos chamam **SQLFetchScroll** para posicionar o cursor e buscar linhas. O **SQLFetchScroll** dá suporte à rolagem relativa (linhas posteriores, anteriores e não relativas a *n* ), rolagem absoluta (primeira, última e linha *n*) e posicionamento por indicador. Os argumentos *FetchOrientation* e *FetchOffset* no **SQLFetchScroll** especificam qual conjunto de linhas deve ser obtido, conforme mostrado nos diagramas a seguir.  
  
 ![Buscando os conjuntos de linhas próximo, anterior, primeiro e último](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **Buscando os conjuntos de linhas próximo, anterior, primeiro e último**  
  
 ![Buscando um conjunto de linhas absoluto, relativo e indicado](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **Buscando conjuntos de linhas absolutos, relativos e marcados**  
  
 **SQLFetchScroll** posiciona o cursor para a linha especificada e retorna as linhas no conjunto de linhas que começa com aquela linha. Se o conjunto de linhas especificado sobrepor o final do conjunto de resultados, um conjunto de linhas parcial será retornado. Se o conjunto de linhas especificado sobrepor o início do conjunto de resultados, o primeiro conjunto de linhas no conjunto de resultados geralmente será retornado; para obter detalhes completos, consulte a descrição da função [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) .  
  
 Em alguns casos, o aplicativo pode querer posicionar o cursor sem recuperar nenhum dado. Por exemplo, talvez queira testar se uma linha existe ou apenas obter o indicador para a linha sem colocar outros dados na rede. Para fazer isso, ele define o atributo da instrução SQL_ATTR_RETRIEVE_DATA como SQL_RD_OFF. A variável associada à coluna de indicador (se houver) é sempre atualizada, independentemente da configuração desse atributo de instrução.  
  
 Depois que o conjunto de linhas for recuperado, o aplicativo poderá chamar **SQLSetPos** para posicioná-lo em uma linha específica no conjunto de linhas ou atualizar linhas no conjunto de linhas. Para obter mais informações sobre como usar o **SQLSetPos**, consulte [atualizando dados com o SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
> [!NOTE]  
>  Há suporte para rolagem no ODBC 2. drivers *x* por **SQLExtendedFetch**. Para obter mais informações, consulte [cursores de bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.
