---
title: Construindo instruções pesquisadas | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8f24fe59da1377ea42900a8f1f0b89eb97125f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019173"
---
# <a name="constructing-searched-statements"></a>Construir instruções pesquisadas
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Para dar suporte à atualização posicionada e instruções delete, a biblioteca de cursores constrói um pesquisada **atualize** ou **excluir** instrução from da instrução posicionada. Para dar suporte a chamadas para **SQLGetData** em um bloco de dados, a biblioteca de cursores constrói um pesquisada **selecione** definido de instrução para criar um resultado que contém a linha atual de dados. Em cada uma dessas instruções, o **onde** cláusula enumera os valores armazenados em cache para cada coluna associada que retorna SQL_PRED_SEARCHABLE ou SQL_PRED_BASIC para o identificador de campo SQL_DESC_SEARCHABLE no  **SQLColAttribute**.  
  
> [!CAUTION]  
>  O **onde** cláusula construída pela biblioteca de cursores para identificar a linha atual pode não conseguir identificar todas as linhas, identifique uma linha diferente ou identificar mais de uma linha.  
  
 Se uma instrução de exclusão ou atualização posicionada afeta mais de uma linha, a biblioteca de cursores atualiza a matriz de status de linha somente para a linha na qual o cursor está posicionado e retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01001 (conflito de operação do Cursor). Se a instrução não identificar todas as linhas, a biblioteca de cursores não atualiza a matriz de status de linha e retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01001 (conflito de operação do Cursor). Um aplicativo pode chamar **SQLRowCount** para determinar o número de linhas que foram atualizadas ou excluídas.  
  
 Se o **selecionar** cláusula usada para posicionar o cursor para uma chamada para **SQLGetData** identifica mais de uma linha, **SQLGetData** não é garantida para retornar os dados corretos. Se ela não identifica quaisquer linhas **SQLGetData** retorne SQL_NO_DATA.  
  
 Se um aplicativo está em conformidade com as diretrizes a seguir, o **onde** cláusula construída pela biblioteca de cursores deve identificar exclusivamente a linha atual, exceto quando isso for impossível, como quando a fonte de dados contém a duplicata linhas.  
  
-   **Associe as colunas que identificam exclusivamente a linha.** Se as colunas associadas não identificar exclusivamente a linha, o **onde** cláusula construída pela biblioteca de cursores pode identificar mais de uma linha. Em uma atualização posicionada ou uma instrução delete, essa cláusula pode causar mais de uma linha a ser atualizada ou excluída. Em uma chamada para **SQLGetData**, essa cláusula pode fazer com que o driver retornar dados para a linha incorreta. Todas as colunas de associação em uma chave exclusiva garante que cada linha é identificada exclusivamente.  
  
-   **Alocar buffers de dados grandes o suficiente que não ocorrer o truncamento.** Cache da biblioteca de cursor é uma cópia dos valores no conjunto de linhas buffers associados ao conjunto de resultados com **SQLBindCol**. Se os dados são truncados quando ele é colocado nesses buffers, ele também será truncado no cache. Um **onde** cláusula construída a partir de valores truncados não pode identificar corretamente a linha de base na fonte de dados.  
  
-   **Especifique os buffers de tamanho de não-nulo para dados binários de C.** A biblioteca de cursores aloca buffers de tamanho no seu somente se de cache a *StrLen_or_IndPtr* argumento **SQLBindCol** não for nulo. Quando o *TargetType* argumento é SQL_C_BINARY, a biblioteca de cursores exige que o comprimento dos dados binários para construir um **onde** cláusula dos dados. Se não houver nenhum buffer de comprimento para uma coluna SQL_C_BINARY e o aplicativo chama **SQLGetData** ou tentar executar uma atualização posicionada ou excluir instrução, os retornos de biblioteca de cursor SQL_ERROR e SQLSTATE SL014 (um posicionadas solicitação foi emitida e nem todos os campos de contagem de coluna foram armazenados em buffer).  
  
-   **Especifique os buffers de tamanho de não-nulo para colunas que permitem valor nulos.** A biblioteca de cursores aloca buffers de tamanho no seu somente se de cache a *StrLen_or_IndPtr* argumento **SQLBindCol** não for nulo. Como SQL_NULL_DATA é armazenado no buffer de comprimento, a biblioteca de cursores pressupõe que qualquer coluna para qual nenhum comprimento do buffer é especificado é não anulável. Se nenhuma coluna de comprimento é especificada para uma coluna que permite valor nula, a biblioteca de cursores constrói uma **onde** cláusula que usa o valor de dados para a coluna. Essa cláusula não identificar corretamente a linha.
