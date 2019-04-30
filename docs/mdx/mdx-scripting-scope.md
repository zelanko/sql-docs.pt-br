---
title: Instrução SCOPE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 497fdfb11ec186ffba56470f2b0ede2ed2f4221a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187531"
---
# <a name="mdx-scripting---scope"></a>Script MDX – SCOPE


  Limita o escopo de instruções MDX especificadas a um subcubo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SCOPE(Subcube_Expression)   
   [ MDX_Statement ]  
END SCOPE  
  
Subcube_Expression ::=(Auxiliary_Subcube [, Auxiliary_Subcube,...n])  
  
Auxiliary_Subcube ::=   
        Limited_Set   
    | Root([dimension_name])   
    | Leaves([dimension_name])  
  
Limited_Set ::=   
        single_tuple   
    | member   
    | Common_Grain_Members   
    | hierarchy.members   
    | level.members   
    | {}   
    | Descendants  
            (  
                  Member  
         , [level  
         [  
            , SELF   
             | AFTER   
                          | BEFORE   
                          | SELF_AND_AFTER   
                          | SELF_AND_BEFORE   
                          | SELF_BEFORE_AFTER   
                          | LEAVES  
                  ]  
            )   
[* <limited set>]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Subcube_Expression*  
 Uma expressão de subcubo do MDX válida.  
  
 *MDX_Statement*  
 Uma instrução MDX válida.  
  
 *Common_Grain_Members*  
 Uma instrução MDX que é avaliada como membros que tem o mesmo grão.  
  
 *single_tuple*  
 Uma única tupla.  
  
## <a name="remarks"></a>Comentários  
 A instrução SCOPE determina o subcubo que será afetado pela execução de uma ou mais instruções MDX. A menos que uma instrução MDX seja incluída em uma instrução SCOPE, o escopo implícito de uma instrução MDX é o cubo inteiro.  
  
> [!NOTE]  
>  Membros escondidos estão expostos em instruções SCOPE.  
  
 Instruções SCOPE criarão subcubos que expõem "buracos" independentemente do **MDX Compatibility** configuração. Por exemplo, a instrução `Scope( Customer.State.members )` pode incluir os estados nos países ou regiões que não contêm os estados, mas para os quais os membros de placeholder invisíveis foram inseridos.  
  
 Os membros calculados e os conjuntos nomeados criados em uma instrução SCOPE não são afetados por essa instrução.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir, de script de cálculo MDX Adventure Works, solução de exemplo define o escopo atual como o trimestre fiscal no ano fiscal de 2005 e a medida cota de vendas e, em seguida, atribui um valor para as células no escopo atual, usando o  **ParallelPeriod** função. O exemplo modifica o escopo usando outra instrução SCOPE e, em seguida, executa outra atribuição usando o [This (MDX)](../mdx/this-mdx.md) função.  
  
```  
Scope   
 (   
    [Date].[Fiscal Year].&[2005],  
    [Date].[Fiscal].[Fiscal Quarter].Members,  
    [Measures].[Sales Amount Quota]  
 ) ;     
  
   This = ParallelPeriod                               
          (   
             [Date].[Fiscal].[Fiscal Year], 1,  
             [Date].[Fiscal].CurrentMember   
          ) * 1.35 ;  
  
/*-- Allocate equally to months in FY 2002 -----------------------------*/  
  
  Scope   
  (   
     [Date].[Fiscal Year].&[2002],  
     [Date].[Fiscal].[Month].Members   
  ) ;     
  
    This = [Date].[Fiscal].CurrentMember.Parent / 3 ;     
  
  End Scope ;     
End Scope ;     
```  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de script MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
