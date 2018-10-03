---
title: Rolando e buscando linhas (ODBC) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 884c798e14964fbcaaf3ca9ba6656f4d62738fe8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642744"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>Rolar e buscar linhas (ODBC)
Ao usar um cursor rolável, aplicativos chamam **SQLFetchScroll** para posicionar as linhas de cursor e fetch. **SQLFetchScroll** oferece suporte à rolagem relativa (próximo, anterior e relativo *n* linhas), a rolagem absoluto (, sobrenome e de linha *n*) e o posicionamento do indicador. O *FetchOrientation* e *FetchOffset* argumentos **SQLFetchScroll** especificar qual conjunto de linhas para buscar, conforme mostrado nos diagramas a seguir.  
  
 ![Em seguida, busca prévia, primeiro e último conjuntos de linhas](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **Buscando o próximo, anterior, primeiros e últimos conjuntos de linhas**  
  
 ![Buscando o conjunto de linhas absoluto, relativo e indicado](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **Buscar conjuntos de linhas absolutos, relativos e indicadores**  
  
 **SQLFetchScroll** posiciona o cursor para a linha especificada e retorna as linhas no conjunto de linhas a partir da linha. Se o conjunto de linhas especificado se sobrepõe o final do conjunto de resultados, um conjunto de linhas parcial será retornado. Se o conjunto de linhas especificado se sobrepõe o início do resultado definido, o primeiro conjunto de linhas no resultado do conjunto é normalmente retornado; Para obter detalhes completos, consulte a [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) descrição da função.  
  
 Em alguns casos, o aplicativo talvez queira posicionar o cursor sem recuperar todos os dados. Por exemplo, ela talvez queira testar se existe uma linha ou apenas obter o indicador da linha sem colocar outros dados pela rede. Para fazer isso, ele define o atributo da instrução SQL_ATTR_RETRIEVE_DATA para SQL_RD_OFF. A variável associada à coluna de indicador (se houver) é sempre atualizada, independentemente da configuração desse atributo de instrução.  
  
 Depois que o conjunto de linhas tiver sido recuperado, o aplicativo pode chamar **SQLSetPos** para posicionar a uma linha específica no conjunto de linhas ou atualizar linhas no conjunto de linhas. Para obter mais informações sobre como usar **SQLSetPos**, consulte [atualizando dados com SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
> [!NOTE]  
>  Rolagem é compatível com ODBC 2. *x* drivers por **SQLExtendedFetch**. Para obter mais informações, consulte [cursores em bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.
