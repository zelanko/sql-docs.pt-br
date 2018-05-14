---
title: Elemento NavigationProperty (CSDLBI) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9db2facd93380fa3d0e011104bb95950e43340fb
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="navigationproperty-element-csdlbi"></a>Elemento NavigationProperty (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  O elemento NavigationProperty é um tipo complexo que estende o tipo Member da CSDL para oferecer suporte à navegação nos modelos de dados de business intelligence.  
  
> [!WARNING]  
>  Esse elemento é usado para relatório e não pode ser modificado ou manipulado.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento NavigationProperty.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|CollectionCaption|Não|Nome plural para fazer referência a um conjunto de instâncias da propriedade de navegação.<br /><br /> Se esse atributo for omitido, será usado o atributo Caption do Member base.|  
  
## <a name="example"></a>Exemplo  
 **Tabela**  
  
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
  
  
