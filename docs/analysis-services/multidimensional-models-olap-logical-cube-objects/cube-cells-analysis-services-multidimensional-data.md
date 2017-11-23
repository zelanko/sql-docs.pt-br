---
title: "Cubo células (Analysis Services - dados multidimensionais) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- storing data [Analysis Services], cells
- hierarchies [Analysis Services], cells
- OLAP objects [Analysis Services], cells
- data members [Analysis Services]
- cubes [Analysis Services], cells
- empty cells [Analysis Services]
- nonleaf members
- cubes [Analysis Services], examples
- storage [Analysis Services], cells
- nonleaf cells
- calculated cells [Analysis Services]
- dimensions [Analysis Services], cells
- cells [Analysis Services]
- leaf members
- leaf cells
ms.assetid: 9945773c-a43b-40d4-91cf-3d2ebc90bca5
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 96d7b596c1434dce62dfd9013f277b182f5ff4c1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="cube-cells-analysis-services---multidimensional-data"></a>Células de cubo (Analysis Services - Dados Multidimensionais)
  Um cubo é composto de células, organizadas por grupos de medidas e dimensões. Uma célula representa a interseção lógica exclusiva em um cubo de um membro de toda dimensão no cubo. Por exemplo, o cubo descrito pelo seguinte diagrama contém um grupo de medidas que tem duas medidas, organizadas juntamente com três dimensões chamadas Origem, Rota e Temporal.  
  
 ![Diagrama de cubo que identifica uma única célula](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro5.gif "diagrama de cubo que identifica uma única célula")  
  
 A única célula sombreada neste diagrama é a interseção dos seguintes membros:  
  
-   O membro ar da dimensão Rota.  
  
-   O membro África da dimensão Origem.  
  
-   O membro 4º trimestre da dimensão Temporal.  
  
-   A medida Pacotes.  
  
## <a name="leaf-and-nonleaf-cells"></a>Células de folha e não folha  
 O valor para uma célula em um cubo pode ser obtido de uma de várias maneiras. No exemplo anterior, o valor na célula pode ser diretamente recuperado da tabela de fatos do cubo, porque todos os membros usados para identificar essa célula são *membros folha*. Um membro folha não tem nenhum membro filho hierarquicamente e, normalmente, faz referência a um único registro em uma tabela de dimensões. Esse tipo de célula é conhecido como um *célula folha*.  
  
 No entanto, uma célula também pode ser identificada usando *membros não folha*. Um membro não folha é um membro que possui um ou mais membros filhos. Nesse caso, o valor da célula é geralmente derivado da agregação de membros filhos associados ao membro não folha. Por exemplo, a interseção dos seguintes membros e dimensões refere-se a uma célula cujo valor é fornecido pela agregação:  
  
-   O membro ar da dimensão Rota.  
  
-   O membro África da dimensão Origem.  
  
-   O membro 2º semestre da dimensão Temporal.  
  
-   O membro Pacotes.  
  
 O membro 2º semestre da dimensão Temporal é um membro não folha. Portanto, todos os valores associados a ele devem ser agregação de valores, como mostrado no diagrama a seguir.  
  
 ![3º e 4º células trimestre para o membro 2º semestre](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro6.gif "3º e 4º células trimestre para o membro 2º semestre")  
  
 Presumindo que as agregações para o 3º e 4º trimestres são somas, o valor de célula especificado é 400, que é o total de todas as células folha sombreadas no diagrama anterior. Como o valor da célula é derivado da agregação de outras células, a célula especificada é considerada um *célula não folha*.  
  
 Os valores de célula derivados de membros que usam rollups personalizados e grupos de membros, além de membros personalizados, são tratados de forma semelhante. Entretanto, os valores de célula para membros calculados são com base em expressões MDX usadas para definir o membro calculado, em alguns casos, pode não haver dados de célula reais envolvidos. Para obter mais informações, consulte [operadores de acúmulo personalizado em dimensões pai-filho](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-custom-rollup-operators.md), [definir fórmulas de membro personalizado](../../analysis-services/multidimensional-models/attribute-properties-define-custom-member-formulas.md), e [cálculos](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md).  
  
## <a name="empty-cells"></a>Células vazias  
 Não é necessário que toda célula no cubo contenha um valor; pode haver interseções em um cubo que não tenham dados. Essas interseções, chamadas células vazias, ocorrem frequentemente em cubos pois nem toda interseção de um atributo de dimensão com uma medida em um cubo contém um registro correspondente na tabela de fatos. A taxa de células vazias em um cubo para o número total de células em um cubo é frequentemente conhecida como o *dispersão* de um cubo.  
  
 Por exemplo, a estrutura do cubo mostrada no diagrama a seguir é semelhante a outros exemplos neste tópico. Entretanto, nesse exemplo, não há remessas para a África para o terceiro trimestre ou para a Austrália no quarto trimestre. Não há dados na tabela de fatos para oferecer suporte às interseções dessas dimensões e medidas; portanto, as células nessas interseções estão vazias.  
  
 ![Diagrama de cubo que identifica células vazias](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro7.gif "diagrama de cubo que identifica células vazias")  
  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], uma célula vazia é uma célula que tem qualidades especiais. Como as células vazias podem distorcer os resultados de interjunções, contagens etc., muitas funções MDX oferecem a habilidade de ignorar as células vazias para fins de cálculo. Para obter mais informações, consulte [expressões multidimensionais &#40; MDX &#41; Referência](../../mdx/multidimensional-expressions-mdx-reference.md), e [principais conceitos em MDX &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md).  
  
## <a name="security"></a>Segurança  
 O acesso a dados de célula é gerenciado no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no nível da função, e pode ser controlado minuciosamente pelo uso de expressões MDX. Para obter mais informações, consulte [conceder acesso personalizado a dimensão de dados &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md), e [conceder acesso personalizado a célula de dados &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Armazenamento de cubo &#40; Analysis Services - dados multidimensionais &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)   
 [Agregações e designs de agregação](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
