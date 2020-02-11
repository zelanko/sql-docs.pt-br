---
title: Desordenar (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 954a71c8ca2e96d905892d77ff12b7270deded5f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097264"
---
# <a name="unorder-mdx"></a>Unorder (MDX)


  Remove qualquer classificação forçada de um conjunto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Unorder(Set_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 A função **desordenar** remove qualquer ordenação imposta nas tuplas contidas no conjunto por qualquer outra função ou instrução, como a função [Order](../mdx/order-mdx.md) . A ordenação das tuplas no conjunto retornado pela função de **desordenação** é indeterminada.  
  
 A função de **desordenação** é usada como uma dica para a otimização de consulta para o processamento de Set. Se a ordem das tuplas dentro de um conjunto não for importante para um cálculo ou uma consulta, o uso da função de **desordenação** poderá proporcionar um benefício de desempenho nesses casos. Por exemplo, a função não [vazia (MDX)](../mdx/nonempty-mdx.md) pode ter um desempenho melhor quando o conjunto fornecido para essa função é desordenado [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] do que se precisar preservar a ordem [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], embora com o, o processador de consultas tente executar essa função automaticamente para muitas funções, como **sum** e **Aggregate**. O benefício de desempenho do uso de **desordenação** é provavelmente apenas perceptível em conjuntos muito grandes que consistem em milhões de tuplas.  
  
## <a name="example"></a>Exemplo  
 O pseudocódigo a seguir ilustra a sintaxe dessa função.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
