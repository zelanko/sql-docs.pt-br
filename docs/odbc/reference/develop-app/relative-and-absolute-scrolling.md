---
title: Rolagem relativa e absoluta | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae0ed5af8d116a3038b55b1e3d68231154c2a35c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300096"
---
# <a name="relative-and-absolute-scrolling"></a>Rolagem relativa e absoluta
A maioria das opções de rolagem em **SQLFetchScroll** posiciona o cursor em relação à posição atual ou a uma posição absoluta. O **SQLFetchScroll** dá suporte à busca do próximo conjunto de linhas anterior, antes, primeiro e último, bem como à busca relativa (busque o conjunto de linha *n* linhas desde o início do conjunto de linhas atual) e a busca absoluta (busque o conjunto de linhas começando na linha *n*). Se *n* for negativo em uma busca absoluta, as linhas serão contadas a partir do final do conjunto de resultados. Portanto, uma busca absoluta da linha-1 significa buscar o conjunto de linhas que começa com a última linha no conjunto de resultados.  
  
 Cursores dinâmicos detectam linhas inseridas e excluídas do conjunto de resultados, portanto, não há uma maneira fácil para cursores dinâmicos recuperarem a linha em um número específico além de ler desde o início do conjunto de resultados, o que provavelmente será lento. Além disso, a busca absoluta não é muito útil em cursores dinâmicos porque os números de linha mudam conforme as linhas são inseridas e excluídas; Portanto, buscar sucessivamente o mesmo número de linha pode produzir linhas diferentes.  
  
 Os aplicativos que usam **SQLFetchScroll** apenas para seus recursos de cursor de bloco, como relatórios, provavelmente passarão pelo conjunto de resultados uma única vez, usando apenas a opção para buscar o próximo conjunto de linhas. Os aplicativos baseados em tela, por outro lado, podem tirar proveito de todos os recursos do **SQLFetchScroll**. Se o aplicativo definir o tamanho do conjunto de linhas como o número de linhas exibidas na tela e associar os buffers de tela ao conjunto de resultados, ele poderá converter as operações da barra de rolagem diretamente em chamadas para **SQLFetchScroll**.  
  
|Operação de barra de rolagem|Opção de rolagem SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Uma página acima|SQL_FETCH_PRIOR|  
|Page Down|SQL_FETCH_NEXT|  
|Uma linha acima|SQL_FETCH_RELATIVE com *FetchOffset* igual a-1|  
|Uma linha abaixo|SQL_FETCH_RELATIVE com *FetchOffset* igual a 1|  
|Caixa de rolagem na parte superior|SQL_FETCH_FIRST|  
|Caixa de rolagem na parte inferior|SQL_FETCH_LAST|  
|Posição aleatória da caixa de rolagem|SQL_FETCH_ABSOLUTE|  
  
 Esses aplicativos também precisam posicionar a caixa de rolagem após uma operação de rolagem, que requer o número de linha atual e o número de linhas. Para o número da linha atual, os aplicativos podem manter o controle do número da linha atual ou chamar **SQLGetStmtAttr** com o atributo SQL_ATTR_ROW_NUMBER para recuperá-lo.  
  
 O número de linhas no cursor, que é o tamanho do conjunto de resultados, está disponível como o SQL_DIAG_CURSOR_ROW_COUNT campo do cabeçalho de diagnóstico. O valor nesse campo é definido somente após **SQLExecute**, **SQLExecDirect**ou **SQLMoreResult** ser chamado. Essa contagem pode ser uma contagem aproximada ou uma contagem exata, dependendo dos recursos do driver. O suporte do driver pode ser determinado chamando **SQLGetInfo** com os tipos de informações de atributos de cursor e verificando se o SQL_CA2_CRC_APPROXIMATE ou SQL_CA2_CRC_EXACT bit é retornado para o tipo de cursor.  
  
 Uma contagem exata de linhas nunca é suportada para um cursor dinâmico. Para outros tipos de cursores, o driver pode dar suporte a contagens de linhas exatas ou aproximadas, mas não ambos. Se o driver não oferecer suporte a contagens de linhas exatas ou aproximadas para um tipo de cursor específico, o campo SQL_DIAG_CURSOR_ROW_COUNT conterá o número de linhas que foram buscadas até o momento. Independentemente do que o driver dá suporte, **SQLFetchScroll** com uma *operação* de SQL_FETCH_LAST fará com que o campo SQL_DIAG_CURSOR_ROW_COUNT contenha a contagem de linhas exata.
