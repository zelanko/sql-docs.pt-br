---
title: Rolagem Relativa e Absoluta | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300096"
---
# <a name="relative-and-absolute-scrolling"></a>Rolagem relativa e absoluta
A maioria das opções de rolagem no **SQLFetchScroll** posiciona o cursor em relação à posição atual ou a uma posição absoluta. **SQLFetchScroll** suporta buscar os próximos, anteriores, primeiros e últimos conjuntos de linhas, bem como busca relativa (buscar as linhas de linha *n* do início do conjunto de linhas atuais) e busca absoluta (buscar o conjunto de linhas a partir da linha *n*). Se *n* for negativo em uma busca absoluta, as linhas são contadas a partir do final do conjunto de resultados. Assim, uma busca absoluta da linha -1 significa buscar o conjunto de linhas que começa com a última linha no conjunto de resultados.  
  
 Os cursores dinâmicos detectam linhas inseridas e excluídas do conjunto de resultados, de modo que não há uma maneira fácil para os cursores dinâmicos recuperarem a linha em um determinado número que não seja a leitura desde o início do conjunto de resultados, o que provavelmente será lento. Além disso, a busca absoluta não é muito útil em cursores dinâmicos porque os números das linhas mudam à medida que as linhas são inseridas e excluídas; portanto, buscar sucessivamente o mesmo número de linha pode render linhas diferentes.  
  
 Os aplicativos que usam **sqlfetchscroll** apenas para seus recursos de cursor de bloco, como relatórios, provavelmente passarão pelo conjunto de resultados uma única vez, usando apenas a opção de buscar o próximo conjunto de linhas. Aplicativos baseados em tela, por outro lado, podem tirar proveito de todos os recursos do **SQLFetchScroll**. Se o aplicativo definir o tamanho do conjunto de linhas para o número de linhas exibidas na tela e vincular os buffers de tela ao conjunto de resultados, ele poderá traduzir as operações da barra de rolagem diretamente para chamadas para **SQLFetchScroll**.  
  
|Operação de barra de rolagem|Opção de rolagem SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Uma página acima|SQL_FETCH_PRIOR|  
|Página para baixo|SQL_FETCH_NEXT|  
|Uma linha acima|SQL_FETCH_RELATIVE com *FetchOffset* igual a -1|  
|Uma linha abaixo|SQL_FETCH_RELATIVE com *FetchOffset* igual a 1|  
|Caixa de rolagem no topo|SQL_FETCH_FIRST|  
|Caixa de rolagem na parte inferior|SQL_FETCH_LAST|  
|Posição aleatória da caixa de rolagem|SQL_FETCH_ABSOLUTE|  
  
 Esses aplicativos também precisam posicionar a caixa de rolagem após uma operação de rolagem, que requer o número da linha atual e o número de linhas. Para o número atual da linha, os aplicativos podem acompanhar o número da linha atual ou ligar para **SQLGetStmtAttr** com o atributo SQL_ATTR_ROW_NUMBER para recuperá-lo.  
  
 O número de linhas no cursor, que é o tamanho do conjunto de resultados, está disponível como o campo SQL_DIAG_CURSOR_ROW_COUNT do cabeçalho de diagnóstico. O valor neste campo é definido somente após **sqlexecute,** **SQLExecDirect**ou **SQLMoreResult** ter sido chamado. Essa contagem pode ser uma contagem aproximada ou uma contagem exata, dependendo das capacidades do driver. O suporte do driver pode ser determinado ligando para **o SQLGetInfo** com os tipos de informações dos atributos do cursor e verificando se o SQL_CA2_CRC_APPROXIMATE ou SQL_CA2_CRC_EXACT bit é devolvido para o tipo de cursor.  
  
 Uma contagem exata de linhas nunca é suportada para um cursor dinâmico. Para outros tipos de cursores, o driver pode suportar contagem de linhas exatas ou aproximadas, mas não ambos. Se o driver não suportar nenhuma linha exata nem aproximada conta para um tipo específico de cursor, o campo SQL_DIAG_CURSOR_ROW_COUNT contém o número de linhas que foram buscadas até agora. Independentemente do suporte do driver, **o SQLFetchScroll** com uma *operação* de SQL_FETCH_LAST fará com que o campo SQL_DIAG_CURSOR_ROW_COUNT contenha a contagem exata de linhas.
