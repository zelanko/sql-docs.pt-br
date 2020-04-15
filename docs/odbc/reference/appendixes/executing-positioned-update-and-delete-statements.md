---
title: Executando declarações de atualização posicionada e exclusão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96a1aa891ef8ba26c6c239cf35e62a8f36018e65
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306997"
---
# <a name="executing-positioned-update-and-delete-statements"></a>Executar instruções de exclusão e atualização posicionadas
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Depois que um aplicativo buscou um bloco de dados com **SQLFetchScroll,** ele pode atualizar ou excluir os dados no bloco. Para executar uma atualização ou exclusão posicionada, o aplicativo:  
  
1.  Chama **SQLSetPos** para posicionar o cursor na linha a ser atualizado ou excluído.  
  
2.  Constrói uma atualização posicionada ou exclui a declaração com a seguinte sintaxe:  
  
     **ATUALIZAR** *nome da tabela*  
  
     **Identificador** *column-identifier* **=** de coluna SET {*expressão* &#124; **NULL**}  
  
     [**,** *identificador* **=** de coluna {*expressão* &#124; **NULL**}]  
  
     **ONDE CORRENTE DO** *cursor-nome*  
  
     **EXCLUIR DO** *nome da tabela* ONDE CORRENTE **DO** *cursor-nome*  
  
     A maneira mais fácil de construir a cláusula **SET** em uma declaração de atualização posicionada é usar marcadores de parâmetros para cada coluna a ser atualizada e usar **SQLBindParameter** para vinculá-los aos buffers do conjunto de linhas para que a linha seja atualizada. Neste caso, o tipo de dados C do parâmetro será o mesmo que o tipo de dados C do buffer de conjunto de linhas.  
  
3.  Atualiza os buffers de conjunto de linhas para a linha atual se ele executar uma declaração de atualização posicionada. Depois de executar com sucesso uma declaração de atualização posicionada, a biblioteca do cursor copia os valores de cada coluna na linha atual para o cache.  
  
    > [!CAUTION]  
    >  Se o aplicativo não atualizar corretamente os buffers do conjunto de linhas antes de executar uma declaração de atualização posicionada, os dados no cache ficarão incorretos após a execução da declaração.  
  
4.  Executa a declaração de atualização ou exclusão posicionada usando uma declaração diferente da declaração associada ao cursor.  
  
    > [!CAUTION]  
    >  A cláusula **WHERE** construída pela biblioteca cursor para identificar a linha atual pode não identificar quaisquer linhas, identificar uma linha diferente ou identificar mais de uma linha. Para obter mais informações, consulte [Construindo declarações pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Todas as instruções de atualização e exclusão posicionadas requerem um nome do cursor. Para especificar o nome do cursor, um aplicativo chama **SQLSetCursorName** antes de o cursor ser aberto. Para usar o nome do cursor gerado pelo driver, um aplicativo chama **SQLGetCursorName** depois que o cursor é aberto.  
  
 Depois que a biblioteca do cursor executa uma declaração de atualização ou exclusão posicionada, a matriz de status, buffers de conjunto de linhas e cache mantidos pela biblioteca do cursor contêm os valores mostrados na tabela a seguir.  
  
|Declaração usada|Valor na matriz de status de linha|Valores em<br /><br /> buffers de conjunto de linhas|Valores em<br /><br /> buffers de cache|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|Atualização posicionada|SQL_ROW_UPDATED|Novos valores[1]|Novos valores[1]|  
|Exclusão posicionada|SQL_ROW_DELETED|Valores antigos|Valores antigos|  
  
 [1] O aplicativo deve atualizar os valores nos buffers de conjunto de linhas antes de executar a declaração de atualização posicionada; depois de executar a declaração de atualização posicionada, a biblioteca do cursor copia os valores nos buffers de conjunto de linhas em seu cache.
