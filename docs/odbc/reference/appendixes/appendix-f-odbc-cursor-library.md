---
title: 'Apêndice F: Biblioteca Cursor ODBC | Microsoft Docs'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292426"
---
# <a name="appendix-f-odbc-cursor-library"></a>Apêndice F: Biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 A biblioteca de cursor ODBC (Odbccr32.dll) suporta cursores roláveis de bloco para qualquer driver que esteja em conformidade com o nível de conformidade da API nível 1 e possa ser redistribuído pelos desenvolvedores com seus aplicativos ou drivers. A biblioteca do cursor também suporta instruções de atualização posicionadas e exclusão de conjuntos de resultados gerados por instruções **SELECT.** Embora suporte apenas cursores estáticos e avançados, a biblioteca do cursor satisfaz as necessidades de muitas aplicações. Além disso, pode proporcionar um bom desempenho, especialmente para conjuntos de resultados de pequeno a médio porte, e para aplicações que não têm bom suporte ao cursor.  
  
 A biblioteca do cursor é uma biblioteca de link dinâmico (DLL) que reside entre o Driver Manager e o driver. Quando um aplicativo chama uma função, o Gerenciador de driver chama a função na biblioteca do cursor, que executa a função ou a chama no driver especificado. Para uma determinada conexão, um aplicativo especifica se a biblioteca do cursor está sempre usada, usada se o driver não suporta cursores roláveis ou nunca usado.  
  
 A biblioteca do cursor aparece como um driver para o Gerenciador de Driver. Se a biblioteca do cursor residir entre o Driver Manager e um driver ODBC *2.x,* a biblioteca do cursor será exibida como um driver ODBC *2.x.* Se a biblioteca do cursor residir entre o Driver Manager e um driver ODBC *3.x,* a biblioteca do cursor será exibida como um driver ODBC *3.x.* O comportamento exibido pela biblioteca do cursor depende da versão do driver com a qual está trabalhando, com exceção das compensações de vinculação, que é suportada tanto para drivers ODBC *2.x* quanto ODBC *3.x.*  
  
 Para implementar cursores de bloco no **SQLFetch** e **no SQLFetchScroll,** a biblioteca do cursor chama repetidamente **sQLFetch** no driver. Para implementar a rolagem, ele armazena os dados que recuperou na memória e nos arquivos de disco. Quando um aplicativo solicita um novo conjunto de linhas, a biblioteca do cursor o recupera conforme necessário do driver ou do cache.  
  
 Para implementar as instruções de atualização e exclusão posicionadas, a biblioteca do cursor constrói uma **instrução UPDATE** ou **DELETE** com uma cláusula **WHERE** que especifica o valor em cache de cada coluna vinculada na linha. Quando executa uma declaração de atualização posicionada, a biblioteca do cursor atualiza seu cache a partir dos valores nos buffers de conjunto de linhas.  
  
 Para obter mais informações sobre a biblioteca do cursor ODBC, consulte as seguintes seções deste apêndice:  
  
-   [Usando a biblioteca de cursores ODBC](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [Executando instruções de exclusão e atualização posicionadas](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [Exemplo de código de biblioteca de cursores](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [Notas de implementação](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [Códigos de erro da Biblioteca de cursores do ODBC](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
