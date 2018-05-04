---
title: Mesclando partições (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a1dffc9450174b44f2e1f935451622a0ef0029ad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="merging-partitions-xmla"></a>Mesclando partições (XMLA)
  Se partições tiverem o mesmo design de agregação e a estrutura, você pode mesclar a partição usando o [MergePartitions](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) do XML for Analysis (XMLA). A mesclagem de partições é uma ação importante a ser executada quando você gerencia partições, principalmente as partições que contêm dados históricos divididos por data.  
  
 Por exemplo, um cubo financeiro pode usar duas partições:  
  
-   Uma partição representa dados financeiros do ano atual, usando configurações de armazenamento ROLAP (OLAP relacional) em tempo real para desempenho.  
  
-   Outra partição contém dados financeiros dos anos anteriores, usando configurações de armazenamento MOLAP (OLAP multidimensional) para armazenamento.  
  
 Ambas as partições utilizam configurações de armazenamento diferentes, mas usam o mesmo design de agregação. Em vez de processar o cubo nos anos de dados históricos no final do ano, você pode usar o **MergePartitions** comando para mesclar a partição para o ano atual para a partição dos anos anteriores. Isso preservará os dados de agregação sem exibir um processamento completo do cubo potencialmente demorado.  
  
## <a name="specifying-partitions-to-merge"></a>Especificando partições para mesclagem  
 Quando o **MergePartitions** comando é executado, os dados de agregação armazenados nas partições de origem especificadas no [fonte](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md) propriedade é adicionada à partição de destino especificada no [destino ](../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md) propriedade.  
  
> [!NOTE]  
>  O **fonte** propriedade pode conter mais de uma referência de objeto de partição. No entanto, o **destino** propriedade não é possível.  
  
 Para ser mescladas com êxito, as partições especificadas em ambos o **fonte** e **destino** devem estar contidos pelo mesmo grupo de medidas e usar o mesmo design de agregação. Caso contrário, ocorre um erro.  
  
 As partições especificadas no **fonte** são excluídos após o **MergePartitions** comando for concluído com êxito.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>Description  
 O exemplo a seguir mescla todas as partições no **Customer Counts** grupo de medidas do **Adventure Works** cubo o **Adventure Works DW** exemplo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de banco de dados para o **Customers_2004** partição.  
  
### <a name="code"></a>Código  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2001</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2002</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2003</PartitionID>  
    </Source>  
  </Sources>  
  <Target>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2004</PartitionID>  
  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
