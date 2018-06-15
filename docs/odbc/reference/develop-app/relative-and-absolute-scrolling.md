---
title: Rolagem relativas e absolutas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93f92b1cd5369ade8102b2505ef37f1da29dde4f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914121"
---
# <a name="relative-and-absolute-scrolling"></a>Rolagem relativas e absolutas
A maioria das opções de rolagem no **SQLFetchScroll** posicionar o cursor em relação à posição atual ou para uma posição absoluta. **SQLFetchScroll** dá suporte à busca o próximo, anterior, primeiro e últimos conjuntos de linhas, como busca bem como relativa (buscar o conjunto de linhas *n* linhas desde o início do conjunto de linhas atual) e da busca absoluta (busca a partir do conjunto de linhas na linha *n*). Se *n* é negativo em uma busca absoluta, as linhas são contadas do final do conjunto de resultados. Portanto, uma busca absoluta da linha -1 significa buscar o conjunto de linhas que começa com a última linha no conjunto de resultados.  
  
 Cursores dinâmicos detectam linhas inseridas e excluídas do conjunto de resultados, portanto, não há nenhuma maneira fácil para cursores dinâmicos recuperar a linha em um determinado número diferente de leitura desde o início do conjunto de resultados, que pode ser lenta. Além disso, busca absoluta não é muito útil para cursores dinâmicos porque os números de linha alterar como as linhas são inseridas e excluídas; Assim, sucessivamente buscar o mesmo número de linha pode gerar linhas diferentes.  
  
 Aplicativos que usam **SQLFetchScroll** apenas para seu bloco funcionalidades de cursor, como relatórios, provavelmente serão passar pelo conjunto de resultados de uma única vez, usando apenas a opção para buscar o próximo conjunto de linhas. Aplicativos baseados em tela, por outro lado, podem tirar proveito dos recursos do **SQLFetchScroll**. Se o aplicativo define o tamanho do conjunto de linhas para o número de linhas exibidas na tela e associa os buffers de tela ao conjunto de resultados, ele poderá converter operações da barra de rolagem diretamente em chamadas para **SQLFetchScroll**.  
  
|Operação de barra de rolagem|Opção de rolagem SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Uma página acima|SQL_FETCH_PRIOR|  
|Página abaixo|SQL_FETCH_NEXT|  
|Uma linha acima|SQL_FETCH_RELATIVE com *FetchOffset* igual a -1|  
|Uma linha abaixo|SQL_FETCH_RELATIVE com *FetchOffset* igual a 1|  
|Caixa de rolagem na parte superior|SQL_FETCH_FIRST|  
|Caixa de rolagem na parte inferior|SQL_FETCH_LAST|  
|Posição aleatória da caixa de rolagem|SQL_FETCH_ABSOLUTE|  
  
 Esses aplicativos também é necessário para a posição da caixa de rolagem após uma operação de rolagem, que exige que o número da linha atual e o número de linhas. Para o número da linha atual, aplicativos podem tanto manter controle do número da linha atual ou chamada **SQLGetStmtAttr** com o atributo SQL_ATTR_ROW_NUMBER recuperá-la.  
  
 O número de linhas no cursor, que é o tamanho do resultado definido, está disponível como o campo SQL_DIAG_CURSOR_ROW_COUNT do cabeçalho de diagnóstico. O valor neste campo é definido somente depois **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResult** foi chamado. Esta contagem pode ser uma contagem aproximada ou uma contagem exata, dependendo dos recursos do driver. O suporte do driver pode ser determinado chamando **SQLGetInfo** com os tipos de informações de atributos de cursor e verificando se o bit SQL_CA2_CRC_APPROXIMATE ou SQL_CA2_CRC_EXACT é retornado para o tipo de cursor.  
  
 Uma contagem de linhas exato nunca é suportada para um cursor dinâmico. Para outros tipos de cursores, o driver pode suportar o contagens de linhas exato ou aproximado, mas não ambos. Se o driver dá suporte nem exato ou aproximado contagens de linha de um tipo de cursor específico, o campo SQL_DIAG_CURSOR_ROW_COUNT contém o número de linhas que foram buscadas até o momento. Independentemente do que o driver dá suporte a, **SQLFetchScroll** com um *operação* de SQL_FETCH_LAST fará com que o campo SQL_DIAG_CURSOR_ROW_COUNT conter o número exato de linhas.
