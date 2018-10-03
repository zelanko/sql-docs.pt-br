---
title: 'Apêndice f: biblioteca de cursores ODBC | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c27845976651b0d68b91b6269a21d1cae3518df8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649584"
---
# <a name="appendix-f-odbc-cursor-library"></a>Apêndice F: Biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 A biblioteca de cursores ODBC (Odbccr32.dll) dá suporte a cursores roláveis do bloco para qualquer driver que está em conformidade com o nível de conformidade com a API do nível 1 e pode ser redistribuída por desenvolvedores com seus aplicativos ou drivers. A biblioteca de cursores também dá suporte a instruções de exclusão e atualização posicionadas para conjuntos de resultados gerados pelo **selecionar** instruções. Embora ela ofereça suporte a apenas Cursores estáticos e somente de encaminhamento, a biblioteca de cursores atende às necessidades de muitos aplicativos. Além disso, ele pode fornecer bom desempenho, especialmente para conjuntos de resultados de empresas de pequeno a médio porte e para aplicativos que não têm suporte de cursor BOM.  
  
 A biblioteca de cursores é uma biblioteca de vínculo dinâmico (DLL) que reside entre o Gerenciador de Driver e o driver. Quando um aplicativo chama uma função, o Gerenciador de Driver chama a função na biblioteca de cursor, que executa a função ou chama no driver especificado. Para uma determinada conexão, um aplicativo especifica se a biblioteca de cursores é sempre usada, usada se o driver não oferece suporte a cursores roláveis ou nunca foi usada.  
  
 A biblioteca de cursor aparece como um driver para o Gerenciador de Driver. Se a biblioteca de cursores reside entre o Gerenciador de Driver e um ODBC 2. *x* driver, a biblioteca de cursor aparece como um ODBC 2. *x* driver. Se a biblioteca de cursores reside entre o Gerenciador de Driver e um ODBC 3 *. x* driver, a biblioteca de cursor aparece como um ODBC 3 *. x* driver. O comportamento exibido pela biblioteca de cursores depende da versão do driver está funcionando, com exceção dos deslocamentos de associação, que tem suporte para ambos os ODBC 2. *x* e o ODBC 3. *x* drivers.  
  
 Para implementar cursores em bloco **SQLFetch** e **SQLFetchScroll**, a biblioteca de cursores chama repetidamente **SQLFetch** no driver. Para implementar a rolagem, ele armazena em cache os dados que ela foi recuperada na memória e nos arquivos de disco. Quando um aplicativo solicita um novo conjunto de linhas, a biblioteca de cursores recupera conforme a necessidade do driver ou o cache.  
  
 Para implementar atualização posicionadas e instruções delete, a biblioteca de cursores constrói uma **atualize** ou **excluir** instrução com uma **onde** cláusula que especifica o armazenados em cache valor de cada coluna associada na linha. Quando ele executa uma instrução de atualização posicionada, a biblioteca de cursores atualiza seu cache entre os valores nos buffers de conjunto de linhas.  
  
 Para obter mais informações sobre a biblioteca de cursores ODBC, consulte as seções a seguir deste apêndice:  
  
-   [Usando a biblioteca de cursores ODBC](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [Executando instruções de exclusão e atualização posicionadas](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [Exemplo de código de biblioteca de cursores](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [Notas de implementação](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [Códigos de erro da Biblioteca de cursores do ODBC](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
