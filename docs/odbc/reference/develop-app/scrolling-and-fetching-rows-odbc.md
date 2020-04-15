---
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
ms.openlocfilehash: 72d262bf73e69388f65ff281e62235d2d831669e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304197"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>Rolar e buscar linhas (ODBC)
Ao usar um cursor rolável, os aplicativos chamam **SQLFetchScroll** para posicionar o cursor e buscar linhas. **SQLFetchScroll** suporta rolagem relativa (próximas, anteriores e *n* linhas relativas), rolagem absoluta (primeira, última e n de *linha)* e posicionamento por marcador. Os argumentos *FetchOrientation* e *FetchOffset* no **SQLFetchScroll** especificam qual conjunto de linhas buscar, conforme mostrado nos diagramas a seguir.  
  
 ![Buscando os conjuntos de linhas próximo, anterior, primeiro e último](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **Buscando os conjuntos de linhas próximo, anterior, primeiro e último**  
  
 ![Buscando um conjunto de linhas absoluto, relativo e indicado](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **Buscando conjuntos de linhas absolutas, relativas e marcadas**  
  
 **SQLFetchScroll** posiciona o cursor para a linha especificada e retorna as linhas no conjunto de linhas começando com essa linha. Se o conjunto de linhas especificado se sobrepor ao final do conjunto de resultados, um conjunto de linhas parcial será retornado. Se o conjunto de linhas especificado se sobrepor ao início do conjunto de resultados, o primeiro conjunto de linhas no conjunto de resultados geralmente será retornado; para obter detalhes completos, consulte a descrição da função [SQLFetchScroll.](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
  
 Em alguns casos, o aplicativo pode querer posicionar o cursor sem recuperar nenhum dado. Por exemplo, ele pode querer testar se uma linha existe ou apenas obter o marcador para a linha sem trazer outros dados através da rede. Para isso, ele define o atributo de declaração SQL_ATTR_RETRIEVE_DATA para SQL_RD_OFF. A variável vinculada à coluna de marcadores (se houver) é sempre atualizada, independentemente da configuração deste atributo de declaração.  
  
 Depois que o conjunto de linhas for recuperado, o aplicativo pode chamar **SQLSetPos** para posicionar-se em uma linha específica no conjunto de linhas ou atualizar linhas no conjunto de linhas. Para obter mais informações sobre o uso de **SQLSetPos,** consulte [Atualizar dados com SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
> [!NOTE]  
>  A rolagem é suportada em ODBC 2. *x* drivers por **SQLExtendedFetch**. Para obter mais informações, consulte [Cursors de bloco, cursores roláveis e compatibilidade retrógrada](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)no apêndice G: Diretrizes do driver para compatibilidade retrógrada.
