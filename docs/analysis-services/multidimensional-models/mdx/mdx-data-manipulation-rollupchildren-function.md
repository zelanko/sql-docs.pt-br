---
title: Trabalhando com a função RollupChildren (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 135ab6e43a0b751639bd1ce1d93bf2183039f713
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208770"
---
# <a name="mdx-data-manipulation---rollupchildren-function"></a>Manipulação de dados MDX – Função RollupChildren
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  A função MDX [RollupChildren](../../../mdx/rollupchildren-mdx.md) acumula os filhos de um membro, aplicando um operador unário diferente a cada um deles, e retorna o valor desse rollup como um número. O operador unário pode ser fornecido por uma propriedade do membro associada ao membro filho ou pode ser uma expressão de cadeia de caracteres fornecida diretamente para a função.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Manipulando dados &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
