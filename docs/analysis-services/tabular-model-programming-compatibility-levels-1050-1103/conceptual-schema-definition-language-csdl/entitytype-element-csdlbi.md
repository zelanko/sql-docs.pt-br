---
title: Elemento EntityType (CSDLBI) | Microsoft Docs
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
ms.assetid: 372e2c13-ec38-4bb1-981c-50758d59a1da
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f5b62cad891d4d02120b3325d57e327e299ef1be
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="entitytype-element-csdlbi"></a>Elemento EntityType (CSDLBI)
  O elemento **EntityType** é um tipo complexo que representa a estrutura de uma entidade de alto nível, como um cliente ou pedido, em um modelo de dados. O elemento **bi:EntityType** estende a definição de [EntityType](http://msdn.microsoft.com/library/bb399206.aspx) usada na [Estrutura de Dados de Entidade](http://msdn.microsoft.com/library/bb399567.aspx).  
  
 Um elemento EntityType deve ser especificado para cada uma das entidades incluídas no modelo de dados. Os subelementos de EntityType descrevem as colunas e medidas na tabela. As relações entre as tabelas são incluídas no **EntityContainer**.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento **EntityType** . Consulte também os atributos aplicáveis ao elemento [EntityType](http://msdn.microsoft.com/library/bb399206.aspx) .  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|Sumário|Não|Uma cadeia de caracteres que contém os possíveis tipos de dados em uma coluna. O valor é derivado do valor de DimensionAttributeTypeEnumType no modelo de dados.<br /><br /> Se o valor de DimensionAttributeTypeEnumType for "ExtendedType", o valor de Contents será derivado do elemento ExtendedType de DimensionAttribute. O cliente não é necessário para responder a esses valores.|  
|DefaultDetails|Não|Uma lista de referências de propriedade que representam o conjunto de colunas na tabela.<br /><br /> Consulte [elemento DefaultDetails &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/defaultdetails-element-csdlbi.md).|  
|DefaultImage|Não|Uma referência a uma coluna que contém a imagem que ilustra a entidade.<br /><br /> Em modelos multidimensionais, esse elemento corresponde a um atributo binário no atributo de dimensão. Se esse atributo estiver presente, o elemento deverá conter exatamente um elemento MemberRef.<br /><br /> Consulte [elemento MemberRef &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md).|  
|DefaultMeasure|Não|Uma referência a uma medida na entidade que deve ser usada como o padrão ao fazer cálculos sobre a entidade. Se não for especificado, SUM será o padrão.<br /><br /> Consulte [elemento MemberRef &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md).|  
|DisplayKey|Não|Uma lista de referências a colunas ou a extremidades de função que constituem um identificador forte que identifica exclusivamente uma instância de entidade.<br /><br /> Consulte [elemento DisplayKey &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/displaykey-element-csdlbi.md).|  
|Hierarquia|Não|Uma lista de hierarquias no modelo.<br /><br /> Consulte [elemento Hierarchy &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/hierarchy-element-csdlbi.md).|  
|ReferenceName|Sim|Um identificador que pode ser usado para fazer referência a essa entidade em uma consulta DAX (Expressões de Análise de Dados).<br /><br /> Se esse atributo não estiver presente, será usado o nome do campo totalmente qualificado da entidade.|  
|SortMembers|Não|Uma lista de propriedades na qual classificar. O atributo SortDirection indica se a ordem é crescente ou decrescente.|  
  
## <a name="contents-element"></a>Elemento Contents  
 O elemento **Contents** é um tipo simples que descreve o tipo de dados na entidade.  
  
 O conteúdo da entidade (coluna) pode ser qualquer um dos seguintes valores:  
  
|Valor|Description|  
|-----------|-----------------|  
|Regular|Normalmente, não definido.|  
|Hora|Atributos que representem períodos de tempo, como anos, semestres, trimestres, meses ou dias.|  
|Geografia|Atributos que representam informações geográficas, como cidades ou CEPs.|  
|Organização|Atributos que representam informações organizacionais, como funcionários ou subsidiárias.|  
|BillOfMaterials|Atributos que representam informações de estoque ou manufatura, como listas de peças para produtos.|  
|Contas|Atributos que representam um plano de contas para fins de geração de relatórios financeiros.|  
|Customers|Atributos que representam informações do cliente ou de contato.|  
|Products|Atributos que representam informações de produto.|  
|Cenário|Atributos que representam informações de planejamento ou de análise estratégica.|  
|Quantitative|Atributos que representam informações quantitativas.|  
|Utilitário|Atributos que representam informações diversas.|  
|Moeda|Contém dados e metadados de moeda.|  
|Rates|Atributos que representam informações de taxa de câmbio.|  
|Canal|Atributos que representam informações de canal.|  
|Promoção|Atributos que representam informações de promoções de marketing.|  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
 O exemplo a seguir mostra a parte da representação CSDLBI na versão 1.1 da tabela Geography usada no modelo de tabela da AdventureWorks. A coluna RowNumber é uma coluna oculta gerada automaticamente como um identificador de linha em modelos de tabela e, portanto, tem o atributo Contents, **RowNumber**.  
  
```  
  
<EntityType   
     Name="DimGeography">  
     <Key>  
        <PropertyRef Name="RowNumber" />  
     </Key>  
     <Property   
        Name="RowNumber"   
        Type="Int64" Nullable="false">  
     <bi:Property   
        Hidden="true"   
        Contents="RowNumber"   
        Stability="RowNumber" />  
     </Property>  
....  
  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 O exemplo a seguir mostra os elementos EntityTypes na versão 1.1 da CSDLBI que representam uma parte de uma dimensão de tempo do cubo Operações da Contoso.  
  
```  
<EntityType   
       Name="CalendarQuarter">  
    <Key>  
       <PropertyRef Name="RowNumber" />  
    </Key>  
  
    <Property Name="RowNumber"   
       Type="Int64"   
       Nullable="false">  
    <bi:Property   
       Hidden="true"   
       Contents="RowNumber"   
       Stability="RowNumber"   
    />  
    </Property>  
  
    <Property Name="CalendarQuarter2"   
       Type="String"   
       MaxLength="Max"   
       Unicode="true"   
       FixedLength="false"   
       Nullable="false">  
    <bi:Property   
       Caption="CalendarQuarter"   
       ReferenceName="CalendarQuarter"   
    />  
    </Property>  
   <bi:EntityType />  
</EntityType>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica para Anotações de BI para CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
