---
title: Elemento EntityContainer (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: e328558e-16b0-4d4a-a79a-fdd3c9493595
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 59be912e2be44fca6e3fd49472f0884f9dfd0782
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126576"
---
# <a name="entitycontainer-element-csdlbi"></a>Elemento EntityContainer (CSDLBI)
  O elemento EntityContainer é um tipo complexo que se baseia no tipo CSDL, EntityContainer, que define uma coleção de entidades em um único modelo de dados. Em um aplicativo business intelligence, o modelo de dados representado por um EntityContainer pode conter várias tabelas com colunas vinculadas por relações, bem como cálculos, medidas e KPIs. Ele é conceitualmente semelhante a um banco de dados ou uma fonte de dados.  
  
 O EntityContainer deve especificar cada um dos tipos de entidade inclusos no modelo de dados, incluindo tabelas e relações. Informações sobre essas entidades de modelo são especificadas por meio da lista de entidades filho do tipo de elemento Entity. Para obter mais informações, consulte [Elemento EntityType &#40;CSDLBI&#41;](entitytype-element-csdlbi.md).  
  
 Propriedades como agrupamento e idioma são definidas no nível de EntityContainer, não em objetos individuais. No entanto, colunas e atributos de texto no modelo podem ter legendas ou traduções em outros idiomas.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela abaixo descreve os elementos e atributos que definem o EntityContainer.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|Nome|Sim|O nome do modelo de dados.|  
|Legenda|não|Uma descrição do banco de dados ou do modelo de dados.|  
|Cultura|Sim|Uma cadeia de caracteres que contém o LCID da solicitação.|  
|CompareOptions|Sim|Classificação específica do idioma e opções de comparação de cadeia de caracteres para o modelo.|  
|DirectQueryMode|não|Uma enumeração que indica o modo de consulta quando o modelo estiver usando o modo DirectQuery.|  
|Elemento EntitySet|Sim|[Elemento EntitySet &#40;CSDLBI&#41;](entityset-element-csdlbi.md)|  
|Elemento AssociationSet|não|[Elemento AssociationSet &#40;CSDLBI&#41;](associationset-element-csdlbi.md)|  
  
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
  
|Valor|Description|  
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
 [Elemento EntitySet &#40;CSDLBI&#41;](entityset-element-csdlbi.md)  
  
  
