---
title: Elemento Hierarchy (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 9debb638-1b28-401b-9499-8f63943863e9
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: f2846424fdf7104c95cb4a56ac836b57583bf0cc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012077"
---
# <a name="hierarchy-element-csdlbi"></a>Elemento Hierarchy (CSDLBI)
  O elemento Hierarchy é um contêiner lógico para os campos em uma tabela que podem ser vinculados entre si para formar uma hierarquia. O elemento Hierarchy é derivado do elemento CSDL Member e foi estendido para oferecer suporte às hierarquias criadas em modelos de dados de business intelligence.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento Hierarchy.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|Documentação|não|Uma descrição da hierarquia.|  
|Nível|Sim|Um ou mais elementos Level que definem as colunas usadas na hierarquia.<br /><br /> Consulte [Elemento Level &#40;CSDLBI&#41;](level-element-csdlbi.md).|  
  
## <a name="remarks"></a>Remarks  
 Em modelos tabulares, as hierarquias são criadas por meio da especificação de relações pai-filho entre colunas na mesma tabela. Para obter mais informações, consulte [Hierarquias &#40;SSAS Tabular&#41;](../../tabular-models/hierarchies-ssas-tabular.md).  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
 O exemplo a seguir, na versão 1.0 da CSDLBI, mostra uma hierarquia no modelo de exemplo da AdventureWorks que foi adicionado à tabela Products.  
  
```  
  
<bi:Hierarchy Name="Categoryy">  
    <bi:Level Name="CategoryName">  
       <bi:Source>  
       <bi:PropertyRef Name="CategoryName" />  
       </bi:Source>  
    </bi:Level>  
    <bi:Level Name="ProductName">  
       <bi:Source>  
       <bi:PropertyRef Name="ProductName" />  
       </bi:Source>  
    </bi:Level>  
</bi:Hierarchy>  
  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra uma hierarquia do cubo Operações de Varejo da Contoso.  
  
```  
  
<bi:Hierarchy Name="Product_Hierarchy" Caption="Product Hierarchy" ReferenceName="Product Hierarchy">  
   <bi:Documentation>  
      <bi:Summary>DESCRIPTION_ProductModelCateg_Hierarchies</bi:Summary>  
   </bi:Documentation>  
  
   <bi:Level Name="ProductLine">  
      <bi:Source>  
      <bi:PropertyRef Name="ProductLine" />  
      </bi:Source>  
   </bi:Level>  
  
   <bi:Level Name="ModelName">  
         <bi:Source>  
      <bi:PropertyRef Name="ModelName" />  
      </bi:Source>  
   </bi:Level>  
</bi:Hierarchy>  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre o modelo de objeto de tabela](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [Compreendendo funções para hierarquias pai-filho em DAX](https://msdn.microsoft.com/library/gg492192(v=sql.120).aspx)   
 [Configurar o &#40;todos os&#41; nível para hierarquias de atributo](../../multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  