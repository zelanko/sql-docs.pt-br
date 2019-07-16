---
title: Executar posicionado instruções Update e Delete | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c69f784c2ce7c29cb49c81bf23f34a9cad12089
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913625"
---
# <a name="executing-positioned-update-and-delete-statements"></a>Executar instruções de exclusão e atualização posicionadas
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Depois que um aplicativo tiver buscado um bloco de dados com **SQLFetchScroll**, ele pode atualizar ou excluir os dados no bloco. Para executar uma atualização posicionada ou exclusão, o aplicativo:  
  
1.  Chamadas **SQLSetPos** para posicionar o cursor na linha a ser atualizada ou excluída.  
  
2.  Constrói uma atualização posicionada ou uma instrução delete com a seguinte sintaxe:  
  
     **UPDATE** *table-name*  
  
     **SET** *column-identifier* **=** {*expression* &#124; **NULL**}  
  
     [ **,** *identificador de coluna* **=** {*expressão* &#124; **nulo**}]  
  
     **WHERE CURRENT OF** *nome de cursor*  
  
     **DELETE FROM** *nome da tabela* **WHERE CURRENT OF** *nome de cursor*  
  
     A maneira mais fácil para construir o **definir** cláusula em uma instrução de atualização posicionada é usar marcadores de parâmetro para cada coluna para ser atualizado e use **SQLBindParameter** associar esses para os buffers de conjunto de linhas para o linha a ser atualizada. Nesse caso, o tipo de dados C do parâmetro será o mesmo que o tipo de dados C do buffer de linhas.  
  
3.  Atualiza os buffers de conjunto de linhas para a linha atual se ele executará uma instrução update posicionadas. Após a execução de uma instrução de atualização posicionada com êxito, a biblioteca de cursores copia os valores de cada coluna na linha atual para seu cache.  
  
    > [!CAUTION]  
    >  Se o aplicativo não atualizar corretamente os buffers de conjunto de linhas antes de executar uma instrução de atualização posicionada, os dados no cache serão incorretos depois que a instrução é executada.  
  
4.  Executa a atualização posicionada ou uma instrução delete usando uma instrução diferente do que a instrução associada com o cursor.  
  
    > [!CAUTION]  
    >  O **onde** cláusula construída pela biblioteca de cursores para identificar a linha atual pode não conseguir identificar todas as linhas, identifique uma linha diferente ou identificar mais de uma linha. Para obter mais informações, consulte [construindo instruções pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Todos os posicionado update e delete instruções exigem um nome de cursor. Para especificar o nome do cursor, um aplicativo chama **SQLSetCursorName** antes que o cursor é aberto. Para usar o nome de cursor gerado pelo driver, um aplicativo chama **SQLGetCursorName** após o cursor é aberto.  
  
 Após o cursor biblioteca executa uma atualização posicionada ou instrução delete, a matriz de status, buffers de conjunto de linhas e cache mantido pela biblioteca de cursores contêm os valores mostrados na tabela a seguir.  
  
|Instrução usada|Valor na matriz de status de linha|Os valores em<br /><br /> buffers de conjunto de linhas|Os valores em<br /><br /> buffers de cache|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|Atualização posicionada|SQL_ROW_UPDATED|Novos valores [1]|Novos valores [1]|  
|Exclusão posicionada|SQL_ROW_DELETED|Valores antigos|Valores antigos|  
  
 [1], o aplicativo deverá atualizar os valores nos buffers de conjunto de linhas antes de executar a instrução de atualização posicionada; Depois de executar a instrução de atualização posicionada, a biblioteca de cursores copia os valores nos buffers de conjunto de linhas em seu cache.
