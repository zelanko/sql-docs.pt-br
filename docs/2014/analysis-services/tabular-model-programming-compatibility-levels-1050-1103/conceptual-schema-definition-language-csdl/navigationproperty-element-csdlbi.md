---
title: Elemento NavigationProperty (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: a36b4d3b-6a6c-489b-8a46-2e6b925b568f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fbb0d38a4bcab7592893aaa63acb1bbb96dac5c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157576"
---
# <a name="navigationproperty-element-csdlbi"></a>Elemento NavigationProperty (CSDLBI)
  O elemento NavigationProperty é um tipo complexo que estende o tipo Member da CSDL para oferecer suporte à navegação nos modelos de dados de business intelligence.  
  
> [!WARNING]  
>  Esse elemento é usado para relatório e não pode ser modificado ou manipulado.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento NavigationProperty.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|CollectionCaption|não|Nome plural para fazer referência a um conjunto de instâncias da propriedade de navegação.<br /><br /> Se esse atributo for omitido, será usado o atributo Caption do Member base.|  
  
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
 [Compreendendo o modelo de objeto de tabela](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
