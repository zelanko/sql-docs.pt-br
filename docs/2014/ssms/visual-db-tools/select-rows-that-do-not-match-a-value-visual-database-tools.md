---
title: Selecionar linhas que não correspondem a um valor (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- search conditions [SQL Server], rows not matching value
- row not matching value [SQL Server]
- NOT operator [Visual Database Tools]
- search criteria [SQL Server], rows not matching value
ms.assetid: 19898578-7b2f-401c-bb8f-9f2a017efdf7
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c0bfc7ef077a3e968ec418430a5b4213c4ef552b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007434"
---
# <a name="select-rows-that-do-not-match-a-value-visual-database-tools"></a>Selecionar linhas que não correspondem a um valor (Visual Database Tools)
  Para localizar linhas que não correspondem a um valor, use o operador NOT.  
  
### <a name="to-find-rows-that-do-not-match-a-value"></a>Para localizar linhas que não correspondem a um valor  
  
1.  Se você ainda não o fez, adicione as colunas ou expressões que pretende usar nos critérios de pesquisa do [Painel Critérios](visual-database-tools.md).  
  
2.  Localize a linha que contém a coluna de dados ou expressão a ser pesquisada e, em seguida, na coluna de grade **Filtro** , digite o operador NOT seguido de um valor de pesquisa.  
  
 Por exemplo, para localizar todas as linhas em uma tabela de `products` em que os valores da coluna de código do produto começam com um caractere diferente de "A", você pode digitar um critério de pesquisa como o seguinte:  
  
```  
NOT LIKE 'A%'  
```  
  
## <a name="see-also"></a>Consulte também  
 [Regras para inserir valores de pesquisa &#40;Visual Database Tools&#41;](rules-for-entering-search-values-visual-database-tools.md)   
 [Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)  
  
  