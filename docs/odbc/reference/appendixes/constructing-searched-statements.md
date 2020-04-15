---
title: Construindo declarações pesquisadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- searched statements [ODBC]
- ODBC cursor library [ODBC], statement processing
- ODBC cursor library [ODBC], searched statements
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- cursor library [ODBC], searched statements
- SQL statements [ODBC], searched statements
ms.assetid: e429254c-c43f-4fbf-98b2-5f1ed53501ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8b9a27aa9fc84aadc6659993de3e12e269631d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284736"
---
# <a name="constructing-searched-statements"></a>Construir instruções pesquisadas
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Para suportar as instruções de atualização e exclusão posicionadas, a biblioteca do cursor constrói uma instrução **UPDATE** ou **DELETE** pesquisada da instrução posicionada. Para suportar chamadas para **SQLGetData** em um bloco de dados, a biblioteca do cursor constrói uma declaração **SELECT** pesquisada para criar um conjunto de resultados contendo a linha atual de dados. Em cada uma dessas declarações, a cláusula **WHERE** enumera os valores armazenados no cache para cada coluna vinculada que retorna SQL_PRED_SEARCHABLE ou SQL_PRED_BASIC para o identificador de campo SQL_DESC_SEARCHABLE no **SQLColAttribute**.  
  
> [!CAUTION]  
>  A cláusula **WHERE** construída pela biblioteca cursor para identificar a linha atual pode não identificar quaisquer linhas, identificar uma linha diferente ou identificar mais de uma linha.  
  
 Se uma declaração de atualização ou exclusão posicionada afetar mais de uma linha, a biblioteca do cursor atualizará a matriz de status da linha apenas para a linha na qual o cursor está posicionado e retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01001 (conflito de operação cursor). Se a declaração não identificar nenhuma linha, a biblioteca do cursor não atualizará a matriz de status da linha e retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01001 (conflito de operação cursor). Um aplicativo pode chamar **sqlrowcount** para determinar o número de linhas que foram atualizadas ou excluídas.  
  
 Se a cláusula **SELECT** usada para posicionar o cursor de uma chamada para **SQLGetData** identificar mais de uma linha, **o SQLGetData** não terá garantia de retornar os dados corretos. Se não identificar nenhuma linha, **o SQLGetData** retorna SQL_NO_DATA.  
  
 Se um aplicativo estiver em conformidade com as seguintes diretrizes, a cláusula **WHERE** construída pela biblioteca do cursor deve identificar exclusivamente a linha atual, exceto quando isso é impossível, como quando a fonte de dados contém linhas duplicadas.  
  
-   **Vincule colunas que identificam exclusivamente a linha.** Se as colunas vinculadas não identificarem exclusivamente a linha, a cláusula **WHERE** construída pela biblioteca do cursor poderá identificar mais de uma linha. Em uma declaração de atualização ou exclusão posicionada, tal cláusula pode fazer com que mais de uma linha seja atualizada ou excluída. Em uma chamada para **SQLGetData**, tal cláusula pode fazer com que o driver retorne os dados para a linha errada. A vinculação de todas as colunas em uma chave única garante que cada linha seja identificada exclusivamente.  
  
-   **Aloque buffers de dados grandes o suficiente para que não ocorra truncação.** O cache da biblioteca do cursor é uma cópia dos valores nos buffers de conjunto de linhas vinculados ao conjunto de resultados com **SQLBindCol**. Se os dados forem truncados quando forem colocados nesses buffers, ele também será truncado no cache. Uma **cláusula WHERE** construída a partir de valores truncados pode não identificar corretamente a linha subjacente na fonte de dados.  
  
-   **Especifique buffers de comprimento não nulos para dados binários C.** A biblioteca do cursor aloca buffers de comprimento em seu cache somente se o *argumento StrLen_or_IndPtr* no **SQLBindCol** não for nulo. Quando o argumento *TargetType* é SQL_C_BINARY, a biblioteca do cursor requer o comprimento dos dados binários para construir uma cláusula **WHERE** a partir dos dados. Se não houver buffer de comprimento para uma coluna de SQL_C_BINARY e o aplicativo chamar **SQLGetData** ou tentar executar uma declaração de atualização ou exclusão posicionada, a biblioteca do cursor retorna SQL_ERROR e SQLSTATE SL014 (uma solicitação posicionada foi emitida e nem todos os campos de contagem de colunas foram protegidos).  
  
-   **Especifique buffers de comprimento não nulos para colunas anuladas.** A biblioteca do cursor aloca buffers de comprimento em seu cache somente se o *argumento StrLen_or_IndPtr* no **SQLBindCol** não for nulo. Como SQL_NULL_DATA é armazenado no buffer de comprimento, a biblioteca do cursor assume que qualquer coluna para a qual nenhum buffer de comprimento é especificado é não anulada. Se nenhuma coluna de comprimento for especificada para uma coluna anulada, a biblioteca do cursor construirá uma cláusula **WHERE** que usa o valor de dados para a coluna. Esta cláusula não identificará corretamente a linha.
