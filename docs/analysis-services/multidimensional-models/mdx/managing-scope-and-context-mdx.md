---
title: Gerenciando escopo e contexto (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [MDX], context
- scope [MDX]
- CALCULATE statement
- This function [MDX]
- SCOPE statement
- scripts [MDX], scope
ms.assetid: 631e7c20-8be9-4c35-8609-76516aef19d1
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0a7878c4c2420a4f49d14e1a3f2121009fc1d5b3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="managing-scope-and-context-mdx"></a>Gerenciando escopo e contexto (MDX)
  No [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], um script de expressões multidimensionais (MDX) pode ser aplicado ao cubo inteiro ou a partes específicas dele, a pontos específicos da execução do script. O script MDX pode adotar uma abordagem em camadas dos cálculos em um cubo usando passagens de cálculo.  
  
> [!NOTE]  
>  Para obter mais informações sobre como as passagens de cálculo podem afetar os cálculos, consulte [Noções básicas sobre a ordem de passagem e a ordem de resolução &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md).  
  
 Para controlar a passagem de cálculo, o escopo e o contexto de um script MDX, use especificamente a instrução CACULATE, a função **This** e a instrução SCOPE.  
  
## <a name="using-the-calculate-statement"></a>Usando a instrução CALCULATE  
 A instrução CALCULATE preenche cada célula do cubo com dados agregados. Por exemplo, o script MDX padrão possui uma única instrução CALCULATE no início do script.  
  
 Para obter mais informações sobre a sintaxe da instrução CALCULATE, consulte [Instrução CALCULATE &#40;MDX&#41;](../../../mdx/mdx-scripting-calculate.md).  
  
> [!NOTE]  
>  Se o script contiver uma instrução SCOPE com uma instrução CALCULATE, a linguagem MDX avaliará a instrução CALCULATE no contexto do subcubo definido pela instrução SCOPE e não com relação ao cubo inteiro.  
  
## <a name="using-the-this-function"></a>Usando a função This  
 A função **This** permite a recuperação do subcubo atual dentro de um script MDX. Use a função **This** para configurar rapidamente o valor de células do subcubo atual para uma expressão MDX. Com frequência, você usará a função **This** em conjunto com a instrução SCOPE para alterar o conteúdo de um subcubo específico durante uma passagem de cálculo específica.  
  
> [!NOTE]  
>  Se o script contiver uma instrução SCOPE com uma função **This** , o MDX avaliará a função **This** no contexto do subcubo definido pela instrução SCOPE e não com relação ao cubo inteiro.  
  
### <a name="this-function-example"></a>Exemplo da função This  
 O exemplo de comando de script MDX a seguir utiliza a função **This** para aumentar o valor da medida Amount, no grupo de medidas Finanças do cubo de exemplo [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)], em 10% para os filhos do membro Redmond da dimensão Customer:  
  
```  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 Para obter mais informações sobre a sintaxe da função **This**, consulte [This &#40;MDX&#41;](../../../mdx/this-mdx.md).  
  
## <a name="using-the-scope-statement"></a>Usando a instrução SCOPE  
 A instrução SCOPE define o subcubo atual que contém outras expressões MDX e instruções em um script MDX e especifica seu escopo. A linguagem MDX avalia essas outras expressões e instruções MDX, incluindo a função **This** e a instrução CALCULATE, no contexto do subcubo.  
  
 Uma instrução SCOPE é dinâmica, mas não é iterativa por natureza. As instruções contidas em uma instrução SCOPO são executadas uma vez, mas o próprio subcubo pode ser determinado dinamicamente. Por exemplo, você tem um cubo chamado CuboExemplo. Ao cubo CuboExemplo, aplica a instrução SCOPE a seguir para definir um subcubo que define o contexto como ALLMEMBERS na dimensão Medidas:  
  
 `SCOPE([Measures].ALLMEMBERS);`  
  
 `THIS = [Measures].ALLMEMBERS.COUNT;`  
  
 `END SCOPE;`  
  
 As instruções e expressões dessa instrução SCOPE são executadas uma vez.  
  
 Agora, um usuário da empresa executa a consulta MDX a seguir que contém uma medida, chamada MedidaExistente, no cubo de CuboExemplo:  
  
 `WITH MEMBER [Measures].[NewMeasure] AS '1'`  
  
 `SELECT`  
  
 `[Measures].ALLMEMBERS ON COLUMNS,`  
  
 `[Customer].DEFAULTMEMBER ON ROWS`  
  
 `FROM`  
  
 `[SampleCube]`  
  
 O conjunto de células retornado pela consulta é semelhante à saída mostrada na tabela a seguir.  
  
||[MedidaExistente]|[NovaMedida]|  
|-|-------------------------|--------------------|  
|[Cliente]. [Todos]|2|2|  
  
 Analisando o conjunto de células retornado, observe como o valor MedidaExistente, incluído na instrução SCOPE do script MDX, foi atualizado dinamicamente depois que a medida NovaMedida foi definida.  
  
 Uma instrução SCOPE pode ser aninhada em outra instrução SCOPE. No entanto, como a instrução SCOPE não é iterativa, a principal finalidade de aninhar instruções SCOPE é subdividir ainda mais um subcubo para um tratamento especial.  
  
### <a name="scope-statement-example"></a>Exemplo da instrução SCOPE  
 O exemplo de script MDX a seguir utiliza uma instrução SCOPE para definir o valor da medida Amount, do grupo de medidas Finance do cubo de exemplo [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] , 10% mais alto para os filhos do membro Redmond da dimensão Customer. No entanto, outra instrução SCOPE altera o subcubo para incluir a medida Quantia para os filhos do ano calendário 2002. Por fim, a medida Quantia é agregada somente a esse subcubo, deixando os valores agregados da medida Quantia dos outros anos calendários inalterados.  
  
```  
/* Calculate the entire cube first. */  
CALCULATE;  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 Para obter mais informações sobre a sintaxe da instrução SCOPE, consulte [Instrução SCOPE &#40;MDX&#41;](../../../mdx/mdx-scripting-scope.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência da linguagem MDX &#40;MDX&#41;](../../../mdx/mdx-language-reference-mdx.md)   
 [O Script básico de MDX &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  

