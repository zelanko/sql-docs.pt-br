---
title: Nível de elemento (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: fdf75c47-77dc-4bdb-9931-8eca198fdb88
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8b932ac5fac719be29bda37f134f9beb06d1483f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104776"
---
# <a name="level-element-csdlbi"></a>Elemento Level (CSDLBI)
  O elemento Level é um tipo complexo que define um único nível em uma hierarquia  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento Level.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|Origem|Sim|Um contêiner para a referência da propriedade.|  
|PropertyRef|Sim|Uma referência a uma propriedade da instância. Outros atributos do nível, como legendas, nome e nome de referência, podem ser tirados da propriedade da instância referenciada. Nesse caso, você não precisa especificá-los no elemento Level.|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre hierarquias em modelos tabulares, consulte [Elemento Hierarchy &#40;CSDLBI&#41;](hierarchy-element-csdlbi.md).  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra a definição de vários níveis em uma hierarquia do exemplo de modelo de tabela da AdventureWorks.  
  
```  
  
<bi:Hierarchy Name="Category">  
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
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra uma hierarquia com vários níveis do cubo Operações da Contoso.  
  
```  
<bi:Hierarchy   
   Name="Product_Hierarchy"   
   Caption="Product Hierarchy"   
   ReferenceName="Product Hierarchy">  
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
 [Noções básicas sobre o modelo de objeto Tabular](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [Compreendendo funções para hierarquias pai-filho em DAX](https://msdn.microsoft.com/library/gg492192(v=sql.120).aspx)   
 [Configurar o &#40;todos os&#41; nível para hierarquias de atributo](../../multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
