---
title: Elemento EntitySet (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: d4703c9e-5594-472e-a85b-0f5bd0d73d6f
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 93f05510fefc720e074db3fbc26e2347b660031e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="entityset-element-csdlbi"></a>Elemento EntitySet (CSDLBI)
  O elemento EntitySet define uma coleção de entidades de um determinado tipo em um modelo de dados da CSDLBI.  
  
 O EntitySet deve especificar cada um dos tipos de entidade inclusos no modelo de dados. Informações sobre essas entidades de modelo são especificadas por meio da lista de entidades filho do tipo de elemento Entity. Para obter mais informações, consulte [Elemento EntityType &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md).  
  
 Propriedades como agrupamento e idioma são definidas no nível de EntityContainer, não em objetos individuais. No entanto, colunas e atributos de texto no modelo podem ter legendas ou traduções em outros idiomas.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela abaixo lista os elementos e atributos que definem um EntitySet.  
  
|Nome do Atributo|É obrigatório|Descrição|  
|--------------------|-----------------|-----------------|  
|Caption|Não|Uma descrição amigável do conjunto de entidades.|  
|CollectionCaption|Não|Uma cadeia de caracteres que contém o nome plural da entidade.|  
|ReferenceName|Não|Contém o nome não mesclado e totalmente qualificado da entidade. Em um modelo multidimensional, isso corresponde ao nome CubeDimension.|  
|Oculto|Não|Indica se a entidade está oculta. Por padrão, as entidades não são ocultas.|  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra as definições das tabelas Date e Geography, do modelo de tabela da AdventureWorks.  
  
```  
  
<EntitySet   
   Name="Date"   
   EntityType="Sandbox. Date">  
<bi:EntitySet />  
</EntitySet>  
  
<EntitySet   
   Name="Geography"   
   EntityType="Sandbox.Geography">  
<bi:EntitySet />  
</EntitySet>  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra os vários elementos EntitySet do cubo Operações de Varejo da Contoso.  
  
```  
  
<EntitySet Name="Outage" EntityType="Sandbox.Outage">  
       <bi:EntitySet />  
</EntitySet>  
  
<EntitySet Name="Store" EntityType="Sandbox.Store">  
     <bi:EntitySet />  
</EntitySet>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica para Anotações de BI para CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
