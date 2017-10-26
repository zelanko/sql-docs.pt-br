---
title: "Construindo instruções de pesquisados | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- searched statements [ODBC]
- ODBC cursor library [ODBC], statement processing
- ODBC cursor library [ODBC], searched statements
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- cursor library [ODBC], searched statements
- SQL statements [ODBC], searched statements
ms.assetid: e429254c-c43f-4fbf-98b2-5f1ed53501ff
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 90464acc97539252ae24aa6f959c16f58465d715
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="constructing-searched-statements"></a>Construindo instruções pesquisadas
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Para oferecer suporte a atualização posicionada e instruções delete, a biblioteca de cursores constrói um pesquisada **atualizar** ou **excluir** instrução da instrução posicionada. Para dar suporte a chamadas para **SQLGetData** em um bloco de dados, a biblioteca de cursores constrói um pesquisada **selecione** definido de instrução para criar um resultado que contém a linha de dados atual. Em cada uma dessas instruções, o **onde** cláusula enumera os valores armazenados em cache para cada coluna associada que retorna SQL_PRED_SEARCHABLE ou SQL_PRED_BASIC para o identificador de campo SQL_DESC_SEARCHABLE no ** SQLColAttribute**.  
  
> [!CAUTION]  
>  O **onde** cláusula construída pela biblioteca de cursores para identificar a linha atual pode não conseguir identificar todas as linhas, identificar uma linha diferente ou identificar mais de uma linha.  
  
 Se uma atualização posicionada ou uma instrução delete afeta mais de uma linha, a biblioteca de cursores atualizará a matriz de status de linha apenas para a linha na qual o cursor está posicionado e retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01001 (conflito de operação de Cursor). Se a instrução não identificar todas as linhas, a biblioteca de cursores não atualiza a matriz de status de linha e retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01001 (conflito de operação de Cursor). Um aplicativo pode chamar **SQLRowCount** para determinar o número de linhas que foram atualizadas ou excluídas.  
  
 Se o **selecione** cláusula usada para posicionar o cursor para uma chamada para **SQLGetData** identifica mais de uma linha, **SQLGetData** não é garantida para retornar os dados corretos. Se não identificar quaisquer linhas, **SQLGetData** retorna SQL_NO_DATA.  
  
 Se um aplicativo está em conformidade com as diretrizes a seguir, o **onde** cláusula construída pela biblioteca de cursores deve identificar exclusivamente a linha atual, exceto quando isso for impossível, como quando a fonte de dados contém duplicado linhas.  
  
-   **Associe colunas que identificam exclusivamente a linha.** Se as colunas associadas não identificar exclusivamente a linha, o **onde** cláusula construída pela biblioteca de cursor pode identificar mais de uma linha. Em uma atualização posicionada ou uma instrução delete, essa cláusula pode causar mais de uma linha a ser atualizada ou excluída. Em uma chamada para **SQLGetData**, essa cláusula pode fazer com que o driver retornar dados para a linha incorreta. Associação de todas as colunas em uma chave exclusiva garante que cada linha é identificada exclusivamente.  
  
-   **Alocar buffers de dados grandes o suficiente que não ocorrerá o truncamento.** Cache da biblioteca de cursor é uma cópia dos valores nos buffers de linhas associados ao conjunto de resultados com **SQLBindCol**. Se os dados são truncados quando ele é colocado nesses buffers, também será truncado no cache. Um **onde** cláusula construída a partir de valores truncados não pode identificar corretamente a linha de base na fonte de dados.  
  
-   **Especifique os buffers de tamanho não nulo para dados binários de C.** A biblioteca de cursores aloca buffers de tamanho em suas que apenas de cache do *StrLen_or_IndPtr* argumento **SQLBindCol** não for nulo. Quando o *TargetType* argumento é SQL_C_BINARY, a biblioteca de cursores requer o comprimento dos dados binários para construir um **onde** cláusula dos dados. Se não houver nenhum buffer de comprimento de uma coluna SQL_C_BINARY e o aplicativo chama **SQLGetData** ou tenta executar uma atualização posicionada ou exclusão da instrução, o retornará de biblioteca de cursor SQL_ERROR e SQLSTATE SL014 (um posicionadas solicitação foi emitida e nem todos os campos de contagem de coluna foram armazenados em buffer).  
  
-   **Especifique os buffers de tamanho não nulo para colunas anuláveis.** A biblioteca de cursores aloca buffers de tamanho em suas que apenas de cache do *StrLen_or_IndPtr* argumento **SQLBindCol** não for nulo. Como SQL_NULL_DATA são armazenados no buffer de comprimento, a biblioteca de cursores pressupõe que qualquer coluna para que nenhum comprimento foi especificado o buffer é não anulável. Se nenhuma coluna de comprimento é especificada para uma coluna permite valor nula, a biblioteca de cursores constrói um **onde** cláusula que usa o valor de dados para a coluna. Essa cláusula não identificar corretamente a linha.

