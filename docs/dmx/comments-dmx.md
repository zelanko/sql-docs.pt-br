---
description: Comentários (DMX)
title: Comentários (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8069241656de868ae2165fa7348b549c8e3308e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431118"
---
# <a name="comments-dmx"></a>Comentários (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Os comentários em DMX (extensões de mineração de dados) são cadeias de caracteres de texto no código do programa que não [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] é executado. Os comentários são também conhecidos como comentários. Os comentários são usados para documentar código ou para desabilitar temporariamente partes de um script ou instrução DMX durante o diagnóstico de um código.  
  
 Usar comentários para documentar código de programa facilita a manutenção do código no futuro. Use comentários para registrar detalhes, como o nome do programa, nome do desenvolvedor que escreveu o código e as datas de alterações significativas do código. Use igualmente os comentários para descrever cálculos complexos ou para explicar um método de programação.  
  
 A seguir, as diretrizes básicas para escrever comentários:  
  
-   É possível usar todos os caracteres alfanuméricos ou símbolos em um comentário. O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignora todos os caracteres constantes de um comentário.  
  
-   Não há um comprimento máximo para um comentário dentro de um script ou instrução. O comentário pode ser composto por uma ou mais linhas.  
  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte aos seguintes tipos de caracteres de comentário:  
  
-   **(barras duplas de avanço).** Use esses caracteres de comentário para gravar um comentário na mesma linha como código que deve ser executado, ou para gravar um comentário em uma linha por si próprio. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] avalia tudo, desde as barras de avanço duplo até o final da linha como parte do comentário. Para criar um comentário de várias linhas, use as barras duplas no início de cada linha de comentário. Para obter mais informações sobre esse caractere de comentário, consulte [barra dupla &#40;comentário&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md).  
  
-   **--(hifens duplos).** Use esses caracteres de comentário para gravar um comentário na mesma linha como código que deve ser executado, ou para gravar um comentário em uma linha por si próprio. O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] avalia tudo que estiver a partir das barras duplas até o final da linha como parte do comentário. Para criar um comentário de várias linhas, use os hífens duplos no início de cada linha de comentário. Para obter mais informações sobre esse caractere de comentário, consulte [--&#40;comentário&#41; &#40;Resumo do DMX&#41;](../dmx/comment-dmx-summary.md).  
  
-   **/\* ... \* /(pares de caracteres de barra invertida-asterisco).** Use esses caracteres de comentário para gravar um comentário na mesma linha como o código que deve ser executado, para gravar um comentário em uma linha por si próprio ou até mesmo para gravar comentários dentro do código executável. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] avalia tudo do par de comentário aberto (/*) para o par de comentário de fechamento ( \* /) como parte do comentário. Para criar um comentário de várias linhas, inicie o comentário com o par de caracteres de comentário aberto (/ \* ) e termine o comentário com o par de caracteres de comentário de fechamento ( \* /). Nenhum outro caractere de comentário deve ser incluído em qualquer linha do comentário. Para obter mais informações sobre esse caractere de comentário, consulte a [barra &#40;comentário&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão gerais &#40;&#41;DMX ](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
