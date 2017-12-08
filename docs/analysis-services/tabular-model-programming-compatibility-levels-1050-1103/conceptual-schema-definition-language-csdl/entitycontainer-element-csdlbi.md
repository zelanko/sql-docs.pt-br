---
title: Elemento EntityContainer (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
ms.assetid: e328558e-16b0-4d4a-a79a-fdd3c9493595
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e5328a9c360fa4465e0bcf53bd0f017447c7c113
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="entitycontainer-element-csdlbi"></a>Elemento EntityContainer (CSDLBI)
  O elemento EntityContainer é um tipo complexo que se baseia no tipo CSDL, EntityContainer, que define uma coleção de entidades em um único modelo de dados. Em um aplicativo business intelligence, o modelo de dados representado por um EntityContainer pode conter várias tabelas com colunas vinculadas por relações, bem como cálculos, medidas e KPIs. Ele é conceitualmente semelhante a um banco de dados ou uma fonte de dados.  
  
 O EntityContainer deve especificar cada um dos tipos de entidade inclusos no modelo de dados, incluindo tabelas e relações. Informações sobre essas entidades de modelo são especificadas por meio da lista de entidades filho do tipo de elemento Entity. Para obter mais informações, consulte [Elemento EntityType &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md).  
  
 Propriedades como agrupamento e idioma são definidas no nível de EntityContainer, não em objetos individuais. No entanto, colunas e atributos de texto no modelo podem ter legendas ou traduções em outros idiomas.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela abaixo descreve os elementos e atributos que definem o EntityContainer.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|Nome|Sim|O nome do modelo de dados.|  
|Caption|Não|Uma descrição do banco de dados ou do modelo de dados.|  
|Cultura|Sim|Uma cadeia de caracteres que contém o LCID da solicitação.|  
|CompareOptions|Sim|Classificação específica do idioma e opções de comparação de cadeia de caracteres para o modelo.|  
|DirectQueryMode|Não|Uma enumeração que indica o modo de consulta quando o modelo estiver usando o modo DirectQuery.|  
|Elemento EntitySet|Sim|[Elemento EntitySet &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)|  
|Elemento AssociationSet|Não|[Elemento AssociationSet &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/associationset-element-csdlbi.md)|  
  
## <a name="compareoptions-element"></a>Elemento CompareOptions  
 O atributo CompareOptions define propriedades de agrupamento que são aplicadas ao modelo de dados. As propriedades definidas por CompareOptions são derivadas das configurações para ordem de classificação, distinção kana e distinção de maiúsculas/minúsculas definidas no banco de dados do Analysis Services em tempo de design de modelo. A tabela a seguir descreve os valores inclusos como parte do atributo CompareOptions.  
  
|Valor|Description|  
|-----------|-----------------|  
|IgnoreCase|Valor booliano que indica se as comparações de cadeias de caracteres devem ignorar maiúsculas e minúsculas.|  
|IgnoreNonSpace|Valor booliano que indica se as comparações de cadeias de caracteres devem ignorar o não espaçamento que combina caracteres, como diacríticos.|  
|IgnoreKanaType|Valor booliano que indica se as comparações de cadeias de caracteres devem ignorar o tipo kana.|  
|IgnoreWidth|Valor booliano que indica se as comparações de cadeias de caracteres devem ignorar a largura do caractere.|  
  
## <a name="directquerymode"></a>DirectQueryMode  
 **DirectQueryMode**  
  
 O tipo simples, DirectQueryMode, define o tipo de consulta que é usado por padrão quando o modelo é habilitado para recuperar dados diretamente de uma fonte de dados relacional. Essa propriedade é aplicável somente a modelos de tabela que são executados no modo DirectQuery. A tabela a seguir lista os valores possíveis da enumeração do modo DirectQuery.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|InMemory|Indica se as consultas no modelo usarão dados no cache.|  
|InMemoryWithDirectQuery|Indica se, por padrão, as consultas no modelo usarão dados da fonte de dados relacional.|  
|DirectQueryWithInMemory|Indica se, por padrão, as consultas no modelo usarão dados no cache.|  
|DirectQuery|Indica se as consultas no modelo usarão dados somente na fonte de dados relacional.|  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, representa uma parte do modelo de dados de tabela da AdventureWorks.  
  
```  
  
<EntityContainer   
     Name="Sandbox">  
   <EntitySet   
       Name="DimEmployee"   
       EntityType="Sandbox.DimEmployee">  
   <bi:EntitySet />  
   </EntitySet>  
  
   <EntitySet   
     Name="DimProduct"   
       EntityType="Sandbox.DimProduct">  
    <bi:EntitySet />  
    </EntitySet>  
  
<bi:EntityContainer Caption="AWSimple" Culture="en-US">  
  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, é um trecho do cubo Operações da Contoso.  
  
```  
  
<EntityContainer   
     Name="Sandbox">  
   <EntitySet   
      Name="Bike"   
      EntityType="Sandbox.Bike">  
    <bi:EntitySet Hidden="true" />  
   </EntitySet>  
…  
<bi:EntityContainer   
   Caption="CSDLTest"   
   Culture="en-US">  
<bi:CompareOptions   
   IgnoreCase="true" />  
</bi:EntityContainer>  
</EntityContainer>  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Elemento EntitySet &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)  
  
  
