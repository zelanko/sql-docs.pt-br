---
title: 'Apêndice F: biblioteca de cursores ODBC | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec7982150bfa805c7093ab445400ef5ad1ee070c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292426"
---
# <a name="appendix-f-odbc-cursor-library"></a>Apêndice F: Biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 A biblioteca de cursores ODBC (Odbccr32. dll) dá suporte a um bloco de cursores rolável para qualquer driver que esteja em conformidade com o nível de conformidade da API de nível 1 e possa ser redistribuído por desenvolvedores com seus aplicativos ou drivers. A biblioteca de cursores também dá suporte a instruções de atualização e exclusão posicionadas para conjuntos de resultados gerados por instruções **Select** . Embora ele dê suporte apenas a cursores estáticos e somente de encaminhamento, a biblioteca de cursores atende às necessidades de muitos aplicativos. Além disso, ele pode fornecer um bom desempenho, especialmente para conjuntos de resultados de tamanho pequeno para médio e para aplicativos que não têm um bom suporte a cursores.  
  
 A biblioteca de cursores é uma DLL (biblioteca de vínculo dinâmico) que reside entre o Gerenciador de driver e o driver. Quando um aplicativo chama uma função, o Gerenciador de driver chama a função na biblioteca de cursores, que executa a função ou a chama no driver especificado. Para uma determinada conexão, um aplicativo especifica se a biblioteca de cursores sempre será usada, usada se o driver não oferecer suporte a cursores roláveis ou nunca usado.  
  
 A biblioteca de cursores aparece como um driver para o Gerenciador de driver. Se a biblioteca de cursores residir entre o Gerenciador de driver e um driver ODBC *2. x* , a biblioteca de cursores aparecerá como um driver ODBC *2. x* . Se a biblioteca de cursores residir entre o Gerenciador de driver e um driver ODBC *3. x* , a biblioteca de cursores aparecerá como um driver ODBC *3. x* . O comportamento exibido pela biblioteca de cursores depende da versão do driver com o qual está trabalhando, com exceção dos deslocamentos de ligação, que tem suporte para os drivers ODBC *2. x* e ODBC *3. x* .  
  
 Para implementar cursores de bloco em **SQLFetch** e **SQLFetchScroll**, a biblioteca de cursores chama repetidamente **SQLFetch** no driver. Para implementar a rolagem, ele armazena em cache os dados recuperados na memória e em arquivos de disco. Quando um aplicativo solicita um novo conjunto de linhas, a biblioteca de cursores a recupera conforme necessário no driver ou no cache.  
  
 Para implementar as instruções UPDATE e DELETE posicionadas, a biblioteca de cursores constrói uma instrução **Update** ou **delete** com uma cláusula **Where** que especifica o valor em cache de cada coluna associada na linha. Quando ele executa uma instrução UPDATE posicionada, a biblioteca de cursores atualiza seu cache dos valores nos buffers de conjunto de linhas.  
  
 Para obter mais informações sobre a biblioteca de cursores ODBC, consulte as seguintes seções deste apêndice:  
  
-   [Usando a biblioteca de cursores ODBC](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [Executando instruções de exclusão e atualização posicionadas](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [Exemplo de código de biblioteca de cursores](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [Notas de implementação](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [Códigos de erro da Biblioteca de cursores do ODBC](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
