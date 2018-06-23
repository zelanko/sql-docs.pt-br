---
title: Elemento EntitySet (CSDLBI) | Microsoft Docs
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
ms.assetid: d4703c9e-5594-472e-a85b-0f5bd0d73d6f
caps.latest.revision: 9
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 243dd308d996f82c9a51c8ae9f7f44cfd473dcb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120424"
---
# <a name="entityset-element-csdlbi"></a>Elemento EntitySet (CSDLBI)
  O elemento EntitySet define uma coleção de entidades de um determinado tipo em um modelo de dados da CSDLBI.  
  
 O EntitySet deve especificar cada um dos tipos de entidade inclusos no modelo de dados. Informações sobre essas entidades de modelo são especificadas por meio da lista de entidades filho do tipo de elemento Entity. Para obter mais informações, consulte [Elemento EntityType &#40;CSDLBI&#41;](entitytype-element-csdlbi.md).  
  
 Propriedades como agrupamento e idioma são definidas no nível de EntityContainer, não em objetos individuais. No entanto, colunas e atributos de texto no modelo podem ter legendas ou traduções em outros idiomas.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela abaixo lista os elementos e atributos que definem um EntitySet.  
  
|Nome do Atributo|É obrigatório|Description|  
|--------------------|-----------------|-----------------|  
|Legenda|não|Uma descrição amigável do conjunto de entidades.|  
|CollectionCaption|não|Uma cadeia de caracteres que contém o nome plural da entidade.|  
|ReferenceName|não|Contém o nome não mesclado e totalmente qualificado da entidade. Em um modelo multidimensional, isso corresponde ao nome CubeDimension.|  
|Hidden|não|Indica se a entidade está oculta. Por padrão, as entidades não são ocultas.|  
  
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
 [Referência técnica para Anotações de BI para CSDL](technical-reference-for-bi-annotations-to-csdl.md)  
  
  