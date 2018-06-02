---
title: Instrução CREATE SUBCUBE (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 730d6f3b1445017cc1b1988c49bda176c6ba4ced
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580738"
---
# <a name="mdx-data-definition---create-subcube"></a>Definição de dados MDX - criar SUBCUBO
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Redefine o espaço de cubo de um cubo ou subcubo especificado em um subcubo especificado. Essa instrução altera o espaço de cubo aparente para operações subsequentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE SUBCUBE Cube_Name AS Select_Statement  
                                                  | NON VISUAL ( Select_Statement )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 A expressão de cadeia de caracteres válida que fornece o nome do cubo ou perspectiva que está sendo restrito, o qual se transforma no nome do subcubo.  
  
 *Select_Statement*  
 Uma expressão SELECT de linguagem MDX válida que não contém as cláusulas WITH, NON EMPTY ou HAVING e não solicita propriedades de dimensão ou célula.  
  
 Consulte [instrução SELECT &#40;MDX&#41; ](../mdx/mdx-data-manipulation-select.md) para obter uma explicação detalhada de sintaxe em instruções Select e o **NON VISUAL** cláusula.  
  
## <a name="remarks"></a>Remarks  
 Quando os membros padrão são excluídos na definição de um subcubo, as coordenadas são alteradas de modo correspondente. Para os atributos que podem ser agregados, o membro padrão é movido para o membro [All]. Para os atributos que não podem ser agregados, o membro padrão é movido para um membro que existe no subcubo. A tabela a seguir contém um exemplo de combinações de subcubo e membro padrão.  
  
|Membro padrão original|Pode ser agregado|Subseleção|Membro padrão revisado|  
|-----------------------------|-----------------------|---------------|----------------------------|  
|Time.Year.All|Sim|{Time.Year.2003}|Nenhuma alteração|  
|Time.Year. [1997]|Sim|{Time.Year.2003}|Time.Year.All|  
|Time.Year. [1997]|não|{Time.Year.2003}|Time.Year. [2003]|  
|Time.Year. [1997]|Sim|{Time.Year.2003, Time.Year.2004}|Time.Year.All|  
|Time.Year. [1997]|não|{Time.Year.2003, Time.Year.2004}|Time.Year.[2003] ou<br /><br /> Time.Year.[2004]|  
  
 Os membros [All] sempre existirão em um subcubo.  
  
 Os objetos de sessão criados no contexto de um subcubo são descartados quando o subcubo é descartado.  
  
 Para obter mais informações sobre subcubos, consulte [criando subcubos em MDX &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir cria um subcubo que restringe o espaço de cubo aparente aos membros que existem com o país Canadá. Ele usa o **MEMBROS** função para retornar todos os membros do país da hierarquia Geografia do definido pelo usuário - retornando somente o Canadá.  
  
```  
CREATE SUBCUBE [Adventure Works] AS  
   SELECT [Geography].[Country].&[Canada] ON 0  
   FROM [Adventure Works]  
  
SELECT [Geography].[Country].[Country].MEMBERS ON 0  
   FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir cria um subcubo que restringe o espaço do cubo aparente a membros {Accessories, Clothing} em Products.Category e {[Value Added Reseller], [Warehouse]} em Resellers.[Business Type].  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works]`  
  
 Consultando o subcubo para todos os membros em Products.Category and Resellers.[Business Type] com o seguinte MDX:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Gera o os seguintes resultados:  
  
|||||  
|-|-|-|-|  
||Todos os Produtos|Acessórios|Clothing|  
|Todos os Revendedores|$2,031,079.39|$506,172.45|$1,524,906.93|  
|Revendedor de Valor Agregado|$767,388.52|$175,002.81|$592,385.71|  
|Warehouse|$1,263,690.86|$331,169.64|$932,521.23|  
  
 Descartar e recriar o subcubo usando a cláusula NON VISUAL criará um subcubo que mantém os totais verdadeiros para todos os membros em Products.Category and Resellers.[Business Type], quer eles estejam visíveis ou não no subcubo.  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 Emitindo a mesma consulta MDX acima:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Gera o os seguintes resultados diferentes:  
  
|||||  
|-|-|-|-|  
||Todos os Produtos|Acessórios|Clothing|  
|Todos os Revendedores|$80,450,596.98|$571,297.93|$1,777,840.84|  
|Revendedor de Valor Agregado|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 A coluna e a linha [All Products] e [All Resellers], respectivamente, contêm totais de todos os membros, não só dos visíveis.  
  
## <a name="see-also"></a>Consulte também  
 [Principais conceitos em MDX &#40;do Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Instruções de script MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [Instrução de SUBCUBO DROP &#40;MDX&#41;](../mdx/mdx-data-definition-drop-subcube.md)   
 [Instrução SELECT &#40;MDX&#41;](../mdx/mdx-data-manipulation-select.md)  
  
  
