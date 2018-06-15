---
title: Estabelecendo o contexto de cubo em uma consulta (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2efdfc74bf45f4e8e6b913e651b0be5fa4511034
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022083"
---
# <a name="establishing-cube-context-in-a-query-mdx"></a>Estabelecendo o contexto de cubo em uma consulta (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Toda consulta MDX é executada em um contexto de cubo especificado. Esse contexto define os membros que são avaliados pelas expressões da consulta.  
  
 Na instrução SELECT, a cláusula FROM determina o contexto de cubo. Esse contexto pode ser o cubo inteiro ou apenas um subcubo dele. Ao especificar o contexto de cubo usando a cláusula FROM, você pode usar funções adicionais para expandir ou restringir esse contexto.  
  
> [!NOTE]  
>  As instruções SCOPE e CALCULATE também permitem administrar o contexto de cubo a partir de um script MDX. Para obter mais informações, consulte [Conceitos básicos do script MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md).  
  
## <a name="from-clause-syntax"></a>Sintaxe da cláusula FROM  
 A sintaxe a seguir descreve a cláusula FROM:  
  
```  
<SELECT subcube clause> ::=  
   Cube_Identifier |   
   (SELECT [  
      * |   
      ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]   
   FROM <SELECT subcube clause> <SELECT slicer axis clause> )  
```  
  
 Nessa sintaxe, observe que é a cláusula `<SELECT subcube clause>` que descreve o cubo ou o subcubo no qual a instrução SELECT é executada.  
  
 Um exemplo simples de uma cláusula FROM seria aquele executado no cubo inteiro de exemplo Adventure Works. Essa cláusula FROM teria o seguinte formato:  
  
```  
FROM [Adventure Works]  
```  
  
 Para obter mais informações sobre a cláusula FROM na instrução MDX SELECT, consulte [Instrução SELECT &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
## <a name="refining-the-context"></a>Refinando o contexto  
 Embora a cláusula FROM especifique o contexto de cubo como um único cubo, ela não impede que você trabalhe com os dados de mais de um cubo ao mesmo tempo.  
  
 Você pode usar a função MDX [LookupCube](../../../mdx/lookupcube-mdx.md) para recuperar dados de cubos fora do contexto de cubo. Além disso, funções, como a função [Filter](../../../mdx/filter-mdx.md) , estão disponíveis para permitir a restrição temporária do contexto durante a avaliação da consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos de consulta MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
