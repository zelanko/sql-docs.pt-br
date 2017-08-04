---
title: Palavras-chave (DMX) reservadas | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- Data Mining Extensions [Analysis Services], reserved keywords
- reserved words [DMX]
- DMX [Analysis Services], reserved keywords
ms.assetid: d74871b0-d33f-4ee0-b1c7-384817c45e66
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f394df445ba40050a55c0b1f6a5c714b1ec4d298
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="reserved-keywords-dmx"></a>Palavras-chave reservadas (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] reserva determinadas palavras-chave para seu uso exclusivo. Essas palavras-chave não podem ser usadas em nenhum lugar nas instruções DMX (Data Mining Extensions), exceto nas posições que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] define na referência de linguagem DMX. As palavras-chave restritas de DMX incluem os seguintes membros:  
  
-   Todas as instruções de definição de dados listados no tópico [instruções de definição de dados DMX](../dmx/dmx-statements-data-definition.md).  
  
-   Todos os dados listadas no tópico de funções de consulta de mineração [referência de função DMX](../dmx/data-mining-extensions-dmx-function-reference.md).  
  
-   Todos os operadores listados no tópico [referência de operador DMX](../dmx/data-mining-extensions-dmx-operator-reference.md).  
  
-   Palavras-chave definidas em linguagem de consulta MDX (Multidimensional Expressions) e que são incluídas como parte de uma instrução DMX.  
  
-   Palavras-chave definidas na especificação do OLE DB for Data Mining e que são incluídas como parte de uma instrução DMX.  
  
 Quando objetos são nomeados em um banco de dados, é recomendado usar uma convenção de nomeação que evite o uso de palavras-chave reservadas.  
  
 Caso o banco de dados não contenha nomes que correspondam às palavras-chave reservadas, será preciso usar identificadores delimitados para fazer referência a esses objetos. Para obter mais informações, consulte [identificadores &#40; DMX &#41;](../dmx/identifiers-dmx.md).  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40; DMX &#41; Referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Noções básicas sobre a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  

