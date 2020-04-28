---
title: Executando instruções UPDATE e DELETE posicionadas | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306997"
---
# <a name="executing-positioned-update-and-delete-statements"></a>Executar instruções de exclusão e atualização posicionadas
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Depois que um aplicativo tiver buscado um bloco de dados com **SQLFetchScroll**, ele poderá atualizar ou excluir os dados no bloco. Para executar uma atualização ou exclusão posicionada, o aplicativo:  
  
1.  Chama **SQLSetPos** para posicionar o cursor na linha a ser atualizada ou excluída.  
  
2.  Constrói uma instrução UPDATE ou DELETE posicionada com a seguinte sintaxe:  
  
     **Atualizar** *tabela-nome*  
  
     **Definir** *coluna-identificador* **=** {*expressão* &#124; **NULL**}  
  
     **=** [**,** *identificador de coluna* {*expressão* &#124; **NULL**}]  
  
     **Onde atual do nome do** *cursor*  
  
     **Excluir do** *nome de tabela* **em que o atual** é o *nome do cursor*  
  
     A maneira mais fácil de construir a cláusula **set** em uma instrução UPDATE posicionada é usar marcadores de parâmetro para cada coluna a ser atualizada e usar **SQLBindParameter** para associá-los aos buffers de conjunto de linhas para a linha a ser atualizada. Nesse caso, o tipo de dados C do parâmetro será o mesmo que o tipo de dados C do buffer do conjunto de linhas.  
  
3.  Atualiza os buffers de conjunto de linhas para a linha atual se ele executar uma instrução UPDATE posicionada. Depois de executar com êxito uma instrução UPDATE posicionada, a biblioteca de cursores copia os valores de cada coluna na linha atual para seu cache.  
  
    > [!CAUTION]  
    >  Se o aplicativo não atualizar corretamente os buffers de conjunto de linhas antes de executar uma instrução UPDATE posicionada, os dados no cache ficarão incorretos após a execução da instrução.  
  
4.  Executa a instrução UPDATE ou DELETE posicionada usando uma instrução diferente da instrução associada ao cursor.  
  
    > [!CAUTION]  
    >  A cláusula **Where** construída pela biblioteca de cursores para identificar a linha atual pode falhar ao identificar quaisquer linhas, identificar uma linha diferente ou identificar mais de uma linha. Para obter mais informações, consulte [construindo instruções pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Todas as instruções UPDATE e DELETE posicionadas exigem um nome de cursor. Para especificar o nome do cursor, um aplicativo chama **SQLSetCursorName** antes de o cursor ser aberto. Para usar o nome do cursor gerado pelo driver, um aplicativo chama **SQLGetCursorName** depois que o cursor é aberto.  
  
 Depois que a biblioteca de cursores executa uma instrução UPDATE ou DELETE posicionada, a matriz de status, os buffers de conjunto de linhas e o cache mantidos pela biblioteca de cursores contêm os valores mostrados na tabela a seguir.  
  
|Instrução usada|Valor na matriz de status da linha|Valores em<br /><br /> buffers de conjunto de linhas|Valores em<br /><br /> buffers de cache|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|Atualização posicionada|SQL_ROW_UPDATED|Novos valores [1]|Novos valores [1]|  
|Exclusão posicionada|SQL_ROW_DELETED|Valores antigos|Valores antigos|  
  
 [1] o aplicativo deve atualizar os valores nos buffers de conjunto de linhas antes de executar a instrução UPDATE posicionada; Depois de executar a instrução UPDATE posicionada, a biblioteca de cursores copia os valores nos buffers de conjunto de linhas para seu cache.
