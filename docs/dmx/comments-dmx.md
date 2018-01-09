---
title: "Comentários (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords:
- comments [DMX]
- Data Mining Extensions [Analysis Services], comments
- double forward slashes
- commenting characters
- text strings [SQL Server]
- remarks [DMX]
- forward slash-asterisk character pairs
- DMX [Analysis Services], comments
- /*...*/ (comment)
- double hyphens
- // (comment)
- -- (comment character)
ms.assetid: 64d10eb5-4fe8-42c6-b387-eff336315e56
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 86fd2ea716fd0366149937af749c240fe01e486d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="comments-dmx"></a>Comentários (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Comentários em extensões DMX (Data Mining) são cadeias de caracteres de texto no programa de código que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não é executado. Os comentários são também conhecidos como comentários. Os comentários são usados para documentar código ou para desabilitar temporariamente partes de um script ou instrução DMX durante o diagnóstico de um código.  
  
 Usar comentários para documentar código de programa facilita a manutenção do código no futuro. Use comentários para registrar detalhes, como o nome do programa, nome do desenvolvedor que escreveu o código e as datas de alterações significativas do código. Use igualmente os comentários para descrever cálculos complexos ou para explicar um método de programação.  
  
 A seguir, as diretrizes básicas para escrever comentários:  
  
-   É possível usar todos os caracteres alfanuméricos ou símbolos em um comentário. O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignora todos os caracteres constantes de um comentário.  
  
-   Não há um comprimento máximo para um comentário dentro de um script ou instrução. O comentário pode ser composto por uma ou mais linhas.  
  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte aos seguintes tipos de caracteres de comentário:  
  
-   **(barras duplas).** Use esses caracteres de comentário para gravar um comentário na mesma linha como código que deve ser executado, ou para gravar um comentário em uma linha por si próprio. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]avalia tudo, desde as barras duplas até o final da linha como parte do comentário. Para criar um comentário de várias linhas, use as barras duplas no início de cada linha de comentário. Para obter mais informações sobre esse caractere de comentário, consulte [barras duplas &#40; Comentário &#41; &#40; DMX &#41; ](../dmx/double-slash-comment-dmx.md).  
  
-   **-(hífens duplos).** Use esses caracteres de comentário para gravar um comentário na mesma linha como código que deve ser executado, ou para gravar um comentário em uma linha por si próprio. O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] avalia tudo que estiver a partir das barras duplas até o final da linha como parte do comentário. Para criar um comentário de várias linhas, use os hífens duplos no início de cada linha de comentário. Para obter mais informações sobre esse caractere de comentário, consulte [-&#40; Comentário &#41; &#40; DMX &#41; Resumo](../dmx/comment-dmx-summary.md).  
  
-   **/\*... \*/ (pares de barra e asterisco caractere).** Use esses caracteres de comentário para gravar um comentário na mesma linha como o código que deve ser executado, para gravar um comentário em uma linha por si próprio ou até mesmo para gravar comentários dentro do código executável. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]avalia tudo, desde o par de comentário de abertura (/ *) para o par de comentário de fechamento (\*/) como parte do comentário. Para criar um comentário de várias linhas, comece o comentário com o par de caracteres de comentário de abertura (/\*) e encerre o comentário com o par de caracteres de comentário de fechamento (\*/). Nenhum outro caractere de comentário deve ser incluído em qualquer linha do comentário. Para obter mais informações sobre esse caractere de comentário, consulte [estrela de barra &#40; Comentário &#41; &#40; DMX &#41; ](../dmx/slash-star-comment-dmx.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões de mineração de dados &#40; DMX &#41; Referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão geral &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e o uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
