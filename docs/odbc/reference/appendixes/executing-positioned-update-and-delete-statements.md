---
title: "Executar posicionado instruções Update e Delete | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 757def8025702d5ca7c867b2d8009c7a1d5cb9a2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="executing-positioned-update-and-delete-statements"></a>Executar instruções de exclusão e atualização posicionada
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Depois que um aplicativo tiver buscado um bloco de dados com **SQLFetchScroll**, ele pode atualizar ou excluir os dados no bloco. Para executar uma atualização posicionada ou exclusão, o aplicativo:  
  
1.  Chamadas **SQLSetPos** para posicionar o cursor na linha a ser atualizada ou excluída.  
  
2.  Constrói uma atualização posicionada ou uma instrução delete com a seguinte sintaxe:  
  
     **ATUALIZAÇÃO** *nome de tabela*  
  
     **DEFINIR** *identificador de coluna*  **=**  {*expressão* &#124; **Nulo**}  
  
     [**,** *identificador de coluna*  **=**  {*expressão* &#124; **Nulo**}]  
  
     **WHERE CURRENT OF** *nome de cursor*  
  
     **DELETE FROM** *nome de tabela* **WHERE CURRENT OF** *nome de cursor*  
  
     A maneira mais fácil para construir o **definir** cláusula em uma instrução de atualização posicionada é usar marcadores de parâmetro para cada coluna para ser atualizado e usar **SQLBindParameter** para associar esses para os buffers de conjunto de linhas para o linha a ser atualizada. Nesse caso, o tipo de dados de C do parâmetro será o mesmo que o tipo de dados C do buffer de linhas.  
  
3.  Atualiza os buffers de conjunto de linhas para a linha atual se ele executará uma instrução update posicionadas. Depois de executar com êxito uma instrução update posicionada, a biblioteca de cursores copia os valores de cada coluna na linha atual em seu cache.  
  
    > [!CAUTION]  
    >  Se o aplicativo não atualizar corretamente os buffers de linhas antes de executar uma instrução update posicionada, os dados no cache estará incorretos depois que a instrução é executada.  
  
4.  Executa a atualização posicionada ou uma instrução delete usando uma instrução diferente que a instrução associada com o cursor.  
  
    > [!CAUTION]  
    >  O **onde** cláusula construída pela biblioteca de cursores para identificar a linha atual pode não conseguir identificar todas as linhas, identificar uma linha diferente ou identificar mais de uma linha. Para obter mais informações, consulte [construindo instruções pesquisados](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Todos os posicionado atualização e instruções delete requerem um nome de cursor. Para especificar o nome de cursor, um aplicativo chama **SQLSetCursorName** antes do cursor é aberto. Para usar o nome de cursor gerado pelo driver, um aplicativo chama **SQLGetCursorName** após o cursor é aberto.  
  
 Após o cursor library executa uma atualização posicionada ou instrução delete, a matriz de status, os buffers de linhas e cache mantido pela biblioteca de cursores contêm os valores mostrados na tabela a seguir.  
  
|Instrução usada|Valor na matriz de status de linha|Valores em<br /><br /> buffers de conjunto de linhas|Valores em<br /><br /> buffers de cache|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|Atualização posicionada|SQL_ROW_UPDATED|Novos valores [1]|Novos valores [1]|  
|Delete posicionada|SQL_ROW_DELETED|Valores antigos|Valores antigos|  
  
 [1], o aplicativo deve atualizar os valores nos buffers de linhas antes de executar a instrução de atualização posicionada; Depois de executar a instrução de atualização posicionada, a biblioteca de cursores copia os valores nos buffers de conjunto de linhas para seu cache.
