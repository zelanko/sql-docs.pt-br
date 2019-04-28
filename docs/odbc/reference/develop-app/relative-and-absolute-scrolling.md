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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ba05cb9079514750cf087149bae476efe0d8d41
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861506"
---
# <a name="relative-and-absolute-scrolling"></a>Rolagem relativa e absoluta
A maioria das opções de rolagem na **SQLFetchScroll** posicionar o cursor em relação à posição atual ou para uma posição absoluta. **SQLFetchScroll** dá suporte à busca o próximo, anterior, primeiros e últimos conjuntos de linhas, como bem como relativo de busca (buscar o conjunto de linhas *n* linhas desde o início do conjunto de linhas atual) e da busca absoluta (busca a partir do conjunto de linhas na linha *n*). Se *n* é negativo em uma busca absoluta, as linhas são contadas do final do conjunto de resultados. Portanto, uma busca absoluta da linha -1 significa buscar o conjunto de linhas que começa com a última linha no conjunto de resultados.  
  
 Cursores dinâmicos detectam linhas inseridos e excluídos do conjunto de resultados, portanto, não há nenhuma maneira fácil para cursores dinâmicos recuperar a linha em um determinado número diferente de leitura desde o início do conjunto de resultados, que pode ser lenta. Além disso, busca absoluta não é muito útil para cursores dinâmicos como números de linha alteram como as linhas são inseridas e excluídas; Portanto, sucessivamente, buscar o mesmo número de linha pode gerar linhas diferentes.  
  
 Aplicativos que usam **SQLFetchScroll** somente para o seu bloco funcionalidades de cursor, como relatórios, provavelmente passarão pelo conjunto de resultados uma vez, usando apenas a opção para buscar o próximo conjunto de linhas. Aplicativos baseados em tela, por outro lado, podem tirar proveito de todos os recursos do **SQLFetchScroll**. Se o aplicativo define o tamanho do conjunto de linhas para o número de linhas exibidas na tela e associa os buffers de tela ao conjunto de resultados, ele poderá converter operações da barra de rolagem diretamente em chamadas para **SQLFetchScroll**.  
  
|Operação de barra de rolagem|Opção de rolagem SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Uma página acima|SQL_FETCH_PRIOR|  
|Página para baixo|SQL_FETCH_NEXT|  
|Uma linha acima|SQL_FETCH_RELATIVE com *FetchOffset* igual a -1|  
|Uma linha abaixo|SQL_FETCH_RELATIVE com *FetchOffset* igual a 1|  
|Caixa de rolagem na parte superior|SQL_FETCH_FIRST|  
|Caixa de rolagem na parte inferior|SQL_FETCH_LAST|  
|Posição aleatória da caixa de rolagem|SQL_FETCH_ABSOLUTE|  
  
 Esses aplicativos também precisam posicionar a caixa de rolagem após uma operação de rolagem, o que exige que o número de linha atual e o número de linhas. Para o número de linha atual, aplicativos podem tanto manter controle do número da linha atual ou chamar **SQLGetStmtAttr** com o atributo SQL_ATTR_ROW_NUMBER para recuperá-la.  
  
 O número de linhas no cursor, que é o tamanho do resultado definido, está disponível como o campo SQL_DIAG_CURSOR_ROW_COUNT do cabeçalho de diagnóstico. O valor nesse campo é definido apenas depois **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResult** foi chamado. Essa contagem pode ser uma contagem aproximada ou uma contagem exata, dependendo dos recursos do driver. O suporte do driver pode ser determinado chamando **SQLGetInfo** com os tipos de informações de atributos de cursor e verificando se o bit SQL_CA2_CRC_APPROXIMATE ou SQL_CA2_CRC_EXACT é retornado para o tipo de cursor.  
  
 Um cursor dinâmico nunca é compatível com uma contagem de linhas exata. Para outros tipos de cursores, o driver pode suportar o contagens de linhas exato ou aproximado, mas não ambos. Se o driver dá suporte a exata nem aproximado contagens de linhas para um tipo de cursor específico, o campo SQL_DIAG_CURSOR_ROW_COUNT contém o número de linhas que foram buscadas até o momento. Independentemente do que o driver dá suporte, **SQLFetchScroll** com um *operação* de SQL_FETCH_LAST fará com que o campo SQL_DIAG_CURSOR_ROW_COUNT conter a contagem exata de linhas.
