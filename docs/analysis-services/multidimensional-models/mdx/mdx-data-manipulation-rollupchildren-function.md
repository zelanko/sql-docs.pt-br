---
title: "Trabalhando com a função RollupChildren (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [MDX], RollupChildren function
- RollupChildren function
- custom member properties [MDX]
- IIf function
ms.assetid: 03c624d4-f277-451d-9995-623a07ea2f86
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1fb9052d74a19941a41a915e12acec04bfc38f1c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-manipulation---rollupchildren-function"></a>Manipulação de dados MDX - função RollupChildren
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]O MDX (Multidimensional Expressions) [RollupChildren](../../../mdx/rollupchildren-mdx.md) função acumula os filhos de um membro, aplicando um operador unário diferente para cada filho e retorna o valor desse acúmulo como um número. O operador unário pode ser fornecido por uma propriedade do membro associada ao membro filho ou pode ser uma expressão de cadeia de caracteres fornecida diretamente para a função.  
  
## <a name="rollupchildren-function-examples"></a>Exemplos da função RollupChildren  
 O uso da função **RollupChildren** em instruções MDX é simples de explicar, mas seu efeito sobre as consultas MDX pode ser bem abrangente.  
  
 O efeito da função **RollupChildren** ocorre em consultas MDX projetadas para executar a análise seletiva dos dados de um cubo existente. Por exemplo, a tabela a seguir contém uma lista de membros filho do membro pai Vendas Líquidas, com seus operadores unários (representados pela propriedade de membro **UNARY_OPERATOR** ) mostrados entre parênteses.  
  
|Membro pai|Membro filho|  
|-------------------|------------------|  
|Vendas Líquidas|Vendas internas (+)<br /><br /> Lucros internos (-)<br /><br /> Exportações (+)<br /><br /> Lucros de exportações (-)|  
  
 O membro pai Vendas líquidas apresenta o total de vendas líquidas menos os valores brutos de vendas internas e exportações, sendo os lucros interno e de exportação subtraídos como parte do acúmulo.  
  
 Porém, você quer gerar uma previsão rápida e fácil das vendas brutas internas e exportações mais 10%, ignorando os lucros interno e de exportações. Para calcular esse valor, você pode usar a função **RollupChildren** de uma destas maneiras: com uma propriedade de membro personalizado ou com a função **IIf** .  
  
### <a name="using-a-custom-member-property"></a>Usando uma propriedade de membro personalizado  
 Se o cálculo acumulado for uma operação realizada com frequência, um método seria criar uma propriedade membro capaz de armazenar o operador que será usado com cada filho para um função específica. A tabela a seguir exibe os operadores unários válidos e descreve o resultado esperado.  
  
|Operador|Resultado|  
|--------------|------------|  
|+|total = total + filho atual|  
|-|total = total – filho atual|  
|*|total = total * filho atual|  
|/|total = total / filho atual|  
|~|O filho não é usado no acúmulo. O valor do filho é ignorado.|  
  
 Por exemplo, uma propriedade de membro chamada **SALES_OPERATOR** poderá ser criada e os seguintes operadores unários serão atribuídos a ela, como mostrado na tabela a seguir.  
  
|Membro pai|Membro filho|  
|-------------------|------------------|  
|Vendas Líquidas|Vendas internas (+)<br /><br /> Lucros internos (~)<br /><br /> Exportações (+)<br /><br /> Lucros de exportações (~)|  
  
 Com essa nova propriedade de membro, a seguinte instrução MDX executaria a operação de estimativa das vendas brutas com rapidez e eficiência (ignorando os lucros interno e de exportação):  
  
```  
RollupChildren([Net Sales], [Net Sales].CurrentMember.Properties("SALES_OPERATOR")) * 1.1  
```  
  
 Quando a função é chamada, o valor de cada filho é aplicado ao total usando o operador armazenado na propriedade membro. Os membros dos retornos interno e externo são ignorados e o total de rollup retornado pela função **RollupChildren** é multiplicado por 1,1.  
  
### <a name="using-the-iif-function"></a>Usando a função IIf  
 Se a operação de exemplo não for comum ou se ela se aplicar a apenas uma consulta MDX, a função [IIf](../../../mdx/iif-mdx.md) poderá ser usada com a função **RollupChildren** para fornecer o mesmo resultado. A consulta MDX a seguir apresenta o mesmo resultado que o exemplo MDX anterior, mas sem reordenar para usar uma propriedade de membro personalizado:  
  
```  
RollupChildren([Net Sales], IIf([Net Sales].CurrentMember.Properties("UNARY_OPERATOR") = "-", "~", [Net Sales].CurrentMember.Properties("UNARY_OPERATOR))) * 1.1  
```  
  
 A instrução MDX analisa o operador unário do membro filho. Se o operador unário for usado em uma subtração (como no caso dos membros dos retornos interno e externo), a função **IIf** substituirá o operador unário til (~). Caso contrário, a função **IIf** utilizará o operador unário do membro filho. Por fim, o total acumulado retornado é então multiplicado por 1,1 para apresentar o valor estimado de vendas brutas internas e exportações.  
  
## <a name="see-also"></a>Consulte Também  
 [Manipulando dados &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
