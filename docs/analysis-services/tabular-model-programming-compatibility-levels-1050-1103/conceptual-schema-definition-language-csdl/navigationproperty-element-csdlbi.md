---
title: Elemento NavigationProperty (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: a36b4d3b-6a6c-489b-8a46-2e6b925b568f
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5b1af93e52bc1a2fbd95059c86f73a0481572399
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="navigationproperty-element-csdlbi"></a>Elemento NavigationProperty (CSDLBI)
  O elemento NavigationProperty é um tipo complexo que estende o tipo Member da CSDL para oferecer suporte à navegação nos modelos de dados de business intelligence.  
  
> [!WARNING]  
>  Esse elemento é usado para relatório e não pode ser modificado ou manipulado.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento NavigationProperty.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|CollectionCaption|Não|Nome plural para fazer referência a um conjunto de instâncias da propriedade de navegação.<br /><br /> Se esse atributo for omitido, será usado o atributo Caption do Member base.|  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
 O exemplo a seguir mostra uma propriedade de navegação na versão 1.1 da CSDLBI que descreve o link entre as tabelas SubCategory do Produto e Produto em um modelo tabular.  
  
```  
  
<NavigationProperty   
    Name="Product_Sub_Category_ProductSubcategoryKey"      
    Relationship="Sandbox.Product_Product_Sub_Category_Product_Sub_Category_ProductSubcategoryKey"  
     FromRole="Product_ProductSubcategoryKey"   
    ToRole="Product_Sub_Category_ProductSubcategoryKey">  
<bi:NavigationProperty   
     ReferenceName="Product Sub-Category_ProductSubcategoryKey" />  
</NavigationProperty>  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 O exemplo a seguir mostra uma propriedade de navegação na versão 1.1 da CSDLBI que descreve a relação entre duas tabelas no cubo Operações da Contoso. A relação conecta as tabelas Categoria de bike e Subcategoria de produto.  
  
```  
  
<NavigationProperty   
     Name="BikeSubcategory_ProductSubcategoryKey"   
     Relationship="Sandbox.Bike_BikeSubcategory_BikeSubcategory_ProductSubcategoryKey"   
     FromRole="Bike_ProductSubcategoryKey"   
     ToRole="BikeSubcategory_ProductSubcategoryKey">  
   <bi:NavigationProperty />  
</NavigationProperty>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre o modelo de objeto de tabela em compatibilidade 1050 1103 por meio de níveis](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  

