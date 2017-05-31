---
title: "Selecionar linhas que não correspondem a um valor (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- search conditions [SQL Server], rows not matching value
- row not matching value [SQL Server]
- NOT operator [Visual Database Tools]
- search criteria [SQL Server], rows not matching value
ms.assetid: 19898578-7b2f-401c-bb8f-9f2a017efdf7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 64c4f182e369f8e51a4b1381c5774c951ea5e738
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="select-rows-that-do-not-match-a-value-visual-database-tools"></a>Selecionar linhas que não correspondem a um valor (Visual Database Tools)
Para localizar linhas que não correspondem a um valor, use o operador NOT.  
  
### <a name="to-find-rows-that-do-not-match-a-value"></a>Para localizar linhas que não correspondem a um valor  
  
1.  Se você ainda não o fez, adicione as colunas ou expressões que pretende usar nos critérios de pesquisa do [Painel Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md).  
  
2.  Localize a linha que contém a coluna de dados ou expressão a ser pesquisada e, em seguida, na coluna de grade **Filtro** , digite o operador NOT seguido de um valor de pesquisa.  
  
Por exemplo, para localizar todas as linhas em uma tabela de `products` em que os valores da coluna de código do produto começam com um caractere diferente de "A", você pode digitar um critério de pesquisa como o seguinte:  
  
```  
NOT LIKE 'A%'  
```  
  
## <a name="see-also"></a>Consulte também  
[Regras para inserção de valores de pesquisa (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Especificar critérios de pesquisa (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

