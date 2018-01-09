---
title: Operadores (sintaxe MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], operators
- operators [MDX]
- precedence [MDX]
- MDX [Analysis Services], operators
ms.assetid: 1ff5a529-88fd-4619-86e1-19fa214650d6
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 87304b4a33daa7d9460983a403136974c46c1f81
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="operators-mdx-syntax"></a>Operadores (sintaxe MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Na linguagem MDX, os operadores permitem executar as seguintes ações:  
  
-   Alterar os dados, permanente ou temporariamente.  
  
-   Procurar valores ou objetos que atendam condições específicas.  
  
-   Implementar uma decisão entre valores ou expressões.  
  
-   Testar condições específicas antes de iniciar ou confirmar uma transação ou antes de executar instruções específicas.  
  
 O MDX oferece suporte para os operadores listados na tabela a seguir:  
  
|Para executar este tipo de operação|Use|  
|---------------------------------------|---------|  
|Atribuir um valor a uma variável ou associar uma coluna de conjunto de resultados a um alias.|[Operadores de atribuição](../mdx/assignment-operators.md)|  
|Adicionar, subtrair, multiplicar, dividir.|[Operadores aritméticos](../mdx/arithmetic-operators.md)|  
|Testar a legitimidade de uma condição, como AND, OR, NOT e XOR.|[Operadores bit a bit](../mdx/bitwise-operators.md)|  
|Comparar um valor com outro valor ou uma expressão.|[Operadores de comparação](../mdx/comparison-operators.md)|  
|Combinar permanente ou temporariamente duas cadeias de caracteres em uma.|[Operadores de concatenação](../mdx/concatenation-operators.md)|  
|Combinar permanente ou temporariamente duas expressões de conjunto em um único conjunto.|[Operadores de conjunto](../mdx/set-operators.md)|  
|Executar uma operação em um operando.|[Operadores unários](../mdx/unary-operators.md)|  
  
> [!NOTE]  
>  Em consultas, qualquer um que possa ver os dados no cubo a ser usado com algum tipo de operador pode executar operações. No entanto, você precisa ter as permissões apropriadas antes de poder alterar os dados com êxito.  
  
 Ao usar vários operadores, a ordem em que o MDX avalia os operadores é importante. Similarmente, o usuário dos operadores pode exigir que apenas um tipo de dados seja convertido em outro tipo de dados antes que os operadores possam ser avaliados.  
  
## <a name="evaluating-complex-expressions"></a>Avaliando expressões complexas  
 Você pode criar uma expressão usando os operadores para combinar várias expressões menores. Nessas expressões complexas, o MDX avalia os operadores na ordem com base na definição de precedência do operador usada pelo [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. O MDX executa os operadores com prioridade mais alta antes de executar os operadores com prioridade mais baixa.  
  
### <a name="understanding-operator-precedence"></a>Entendendo a prioridade dos operadores  
 A lista a seguir mostra a prioridade dos operadores, da mais alta para a mais baixa. Os operadores que estão na mesma linha têm a mesma prioridade e são avaliados da esquerda para a direita, a não ser que seja definido de outro modo pelos parênteses:  
  
-   IS  
  
-   AS  
  
-   DISTINCT  
  
-   :  
  
-   ^  
  
-   /, *  
  
-   +, -  
  
-   EXISTING  
  
-   <>, >=, =, \<=, >, <  
  
-   NOT  
  
-   AND  
  
-   XOR  
  
-   OU  
  
 Para obter mais informações sobre operadores em MDX, consulte [referência de operador de MDX &#40; MDX &#41; ](../mdx/mdx-operator-reference-mdx.md).  
  
### <a name="determining-results"></a>Determinando resultados  
 Ao combinar expressões simples para formar uma expressão complexa, as regras dos operadores combinadas com as regras de prioridade do tipo de dados determinam o tipo de dados do valor resultante.  
  
 Se o resultado for um caractere ou valor Unicode, as regras dos operadores combinadas com as regras de prioridade dos agrupamentos determinam o agrupamento do resultado. Para obter mais informações sobre agrupamentos, consulte [idiomas e agrupamentos &#40; Analysis Services &#41; ](../analysis-services/languages-and-collations-analysis-services.md).  
  
 Há também regras que determinam a precisão, a escala e a extensão do resultado, com base na precisão, na escala e na extensão das expressões simples.  
  
## <a name="converting-data-types"></a>Convertendo tipos de dados  
 O MDX converte implicitamente um objeto em um tipo diferente quando esse objeto é usado em uma expressão que requer um tipo diferente. A tabela a seguir define as regras de conversão para cada objeto.  
  
|Tipo original|Tipo necessário|Conversão|  
|-------------------|-----------------|----------------|  
|Nível|Defina|\<nível >. Members|  
|Hierarquia|Membro|\<hierarquia > .defaultmember|  
|Membro|Tupla|(\<Membro >)|  
|Tupla|Membro|\<tupla > .item(0)|  
|Tupla|Escalar|\<tupla > Value|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Elementos de sintaxe MDX &#40; MDX &#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
