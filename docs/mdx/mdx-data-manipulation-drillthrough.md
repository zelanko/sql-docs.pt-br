---
title: "Instrução DRILLTHROUGH (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DRILLTHROUGH
dev_langs:
- kbMDX
helpviewer_keywords:
- DRILLTHROUGH statement
- retrieving data
- data retrieval [MDX]
ms.assetid: dfa22755-0ed4-4bba-9c31-7ade26d9ebdb
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6beadd42ec1f41ccec1ce8b0df999897b50568f5
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-manipulation---drillthrough"></a>Manipulação de dados MDX - DETALHAMENTO
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Recupera as linhas da tabela subjacente que foram usadas para criar uma célula especificada em um cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DRILLTHROUGH[MAXROWSUnsigned_Integer]   
      <MDX SELECT statement>   
      [RETURNSet_of_Attributes_and_Measures   
            [,Set_of_Attributes_and_Measures ...]  
      ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Unsigned_Integer*  
 Um valor inteiro positivo.  
  
 *Instrução MDX SELECT*  
 Toda instrução SELECT das expressões de MDX (Expressions Multidimensional) válidas.  
  
 *Set_of_Attributes_and_Measures*  
 Uma lista de atributos de dimensão e medidas separada por vírgulas.  
  
## <a name="remarks"></a>Comentários  
 Drillthrough é uma operação na qual o usuário final seleciona uma célula a partir de um cubo e recupera um conjunto de resultados a partir dos dados de origem dessa célula para obter informações mais detalhadas. Por padrão, um conjunto de resultados de drillthrough é derivado das linhas da tabela que foram avaliadas para calcular o valor da célula do cubo selecionado. Para que os usuário finais executem o drillthrough, seus aplicativos cliente devem oferecer suporte a esse recurso. Em [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], os resultados são recuperados diretamente do armazenamento MOLAP, a menos que as partições ou dimensões ROLAP são consultados.  
  
> [!IMPORTANT]  
>  A segurança do drillthrough baseia-se nas opções de segurança gerais definidas no cubo. Caso um usuário não consiga alguns dados usando o MDX, o drillthrough também limitará o usuário exatamente da mesma maneira.  
  
 Uma instrução MDX especifica a célula de assunto. O valor especificado pelo **MAXROWS** argumento indica o número máximo de linhas que devem ser retornados pelo conjunto de linhas resultante.  
  
 Por padrão, o número máximo de linhas retornadas é 10.000. Isso significa que, se você deixar **MAXROWS** não for especificado, você obterá 10.000 linhas ou menos. Se esse valor é muito baixo para seu cenário, você pode definir **MAXROWS** para um número mais alto, como `MAXROWS 20000`. Se ele for baixo demais em geral, você pode aumentar o padrão alterando o **OLAP\Query\DefaultDrillthroughMaxRows** propriedade do servidor. Para obter mais informações sobre como alterar essa propriedade, consulte [propriedades de servidor do Analysis Services](../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 A menos que o contrário seja especificado, as colunas retornadas devem incluir todos os atributos de granularidade de todas as dimensões relacionadas ao grupo de medidas da medida especificada, em vez das dimensões muitos para muitos. As dimensões de cubo são precedidas por $ para que possam ser diferenciadas de dimensões e grupos de medidas. O **retornar** cláusula é usada para especificar as colunas retornadas pela consulta de detalhamento. As funções a seguir podem ser aplicadas a um único atributo ou medida pelo **retornar** cláusula.  
  
 Name(attribute_name)  
 Retorna o nome do membro de atributo especificado.  
  
 UniqueName(attribute_name)  
 Retorna o nome exclusivo do membro de atributo especificado.  
  
 Key(attribute_name[, N])  
 Retorna a chave do membro de atributo especificado, onde N especifica a coluna na chave composta (se houver). O valor padrão para N é 1.  
  
 Caption(attribute_name)  
 Retorna a legenda do membro de atributo especificado.  
  
 MemberValue(attribute_name)  
 Retorna o valor de membro do membro de atributo especificado.  
  
 CustomRollup(attribute_name)  
 Retorna a expressão de acúmulo personalizado do membro de atributo especificado.  
  
 CustomRollupProperties(attribute_name)  
 Retorna as propriedades de acúmulo personalizado do membro de atributo especificado.  
  
 UnaryOperator(attribute_name)  
 Retorna o operador unário do membro de atributo especificado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir especifica a célula do mês de julho de 2007 para a medida de valor das vendas do revendedor (medida padrão) da Austrália. A cláusula RETURN faz com que a data de cada venda, o nome do modelo do produto, o nome do funcionário, o valor da venda, o valor do imposto e o valor de custo do produto subjacentes a essa célula sejam retornados.  
  
```  
DRILLTHROUGH  
SELECT  
   ([Date].[Calendar].[Month].[July 2007])  
ON 0   
FROM [Adventure Works]  
WHERE [Geography].[Country].[Australia]  
RETURN   
  [$Date].[Date]  
  ,KEY([$Product].[Model Name])  
  ,NAME([$Employee].[Employee])  
  ,[Reseller Sales].[Reseller Sales Amount]  
  ,[Reseller Sales].[Reseller Tax Amount]  
  ,[Reseller Sales].[Reseller Standard Product Cost]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instruções MDX de manipulação de dados &#40; MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  

