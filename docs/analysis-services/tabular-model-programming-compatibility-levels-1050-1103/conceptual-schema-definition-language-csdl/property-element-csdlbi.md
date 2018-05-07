---
title: Elemento Property (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: f0770c5e-6420-4d0c-a5bf-b94eaf6877ca
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e559d3d8bd56012472d94f0e2fb63067fa08560b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="property-element-csdlbi"></a>Elemento Property (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  O elemento Property na CSDLBI é um tipo complexo que fornece adições ao elemento CSDL Property, como suporte dos modelos de dados de business intelligence.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento CSDLBI Property.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|Sumário|Não|Uma cadeia de caracteres que contém o LCID da solicitação.|  
|DefaultAggregationFunction|Sim|Uma cadeia de caracteres que especifica a função de agregação que deverá ser usada se os cálculos forem executados no atributo e nenhuma outra função tiver sido especificada.<br /><br /> Se não for especificada, será usada a agregação padrão do modelo, que geralmente é SUM.|  
|GroupingBehavior|Não|Um valor que especifica como os resultados da consulta são agrupados. O conteúdo do atributo é definido pelo tipo simples TGroupingBehavior (veja a tabela abaixo).|  
|OrderBy|Não|Uma referência a outra propriedade dentro do modelo que define a ordem de classificação para os valores da propriedade em questão.<br /><br /> Os valores para as duas propriedades DEVEM ter um mapeamento de um para um. Caso contrário, o comportamento da classificação será indefinida.<br /><br /> Se esse elemento for omitido, as propriedades serão classificadas com base em seus valores.|  
|Stability|Não|Um atributo que especifica a estabilidade dos valores da propriedade entre operações de atualização.<br /><br /> Esse atributo não é definido pelos usuários, mas é emitido pelo ambiente no tempo de design apenas para valores instáveis. Ele sempre é aplicado a colunas que contêm um número de linha e a colunas que contêm fórmulas que geram resultados indeterminados, como NOW() ou RAND().<br /><br /> Os valores desse atributo são listados na tabela abaixo, que descreve o tipo simples Stability.|  
  
## <a name="groupingbehavior"></a>GroupingBehavior  
 A tabela a seguir lista os valores do tipo simples GroupingBehavior.  
  
|Valor|Description|  
|-----------|-----------------|  
|GroupOnValue|Agrupe pelo valor do atributo xthe.|  
|GroupOnEntityKey|Agrupe pela chave de entidade.|  
  
 O exemplo a seguir ilustra o uso desses dois valores. Suponha que a consulta foi criada para retornar deduções da folha de pagamento de um determinado usuário, especificado por nome. Supondo que o banco de dados contenha dois usuários com o mesmo nome, mas diferentes identificadores de banco de dados, os resultados da consulta serão diferentes, o que dependerá de qual valor de atributo será aplicado à coluna:  
  
-   **GroupOnValue**: consulta os resultados incluem as deduções da folha de pagamento de ambos os usuários, totalizadas juntas.  
  
-   **GroupOnEntityKey**: consulta resultados incluem as deduções da folha de pagamento para cada usuário, mas listadas individualmente.  
  
## <a name="stability"></a>Stability  
 A tabela a seguir lista os valores de **estabilidade** tipo simples.  
  
|Value|Description|  
|-----------|-----------------|  
|Stable|A propriedade permanece constante entre operações de atualização.|  
|RowNumber|A propriedade contém um número de linha.|  
|Volatile|A propriedade pode não permanecer constante entre operações de atualização.|  
  
## <a name="example"></a>Exemplo  
 **Tabela**  
  
 O XML a seguir mostra a representação, na versão 1.1 da CSDLBI, de algumas propriedades no exemplo de modelo de tabela da AdventureWorks.  
  
```  
  
<EntityType   
   Name="DimEmployee">  
   <Key>  
      <PropertyRef   
      Name="RowNumber" />  
   </Key>  
  
   <Property   
      Name="RowNumber"   
      Type="Int64"   
      Nullable="false">  
   <bi:Property   
      Hidden="true"   
      Contents="RowNumber"   
      Stability="RowNumber" />  
   </Property>  
  
   <Property   
      Name="EmployeeKey"   
      Type="Int64">  
   <bi:Property />  
   </Property>  
….  
</bi:EntityType>  
</EntityType>  
  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra algumas propriedades das colunas no modelo de dados que representa o cubo Operações da Contoso. Observe que as anotações de BI não são exigidas nem aplicadas à maioria das colunas, somente àquelas que exigem tratamento especial na camada de apresentação.  
  
```  
  
<EntityType   
   Name="Bike">  
  
   <Key>  
      <PropertyRef Name="RowNumber" />  
   </Key>  
  
   <Property   
      Name="RowNumber"   
      Type="Int64"   
      Nullable="false">  
   <bi:Property   
      Hidden="true"   
      Contents="RowNumber"   
      Stability="RowNumber"   
   />  
   </Property>  
  
   <Property   
      Name="ProductAlternateKey"   
      Type="String"   
      MaxLength="Max"   
      Unicode="true"   
      FixedLength="false">  
   <bi:Property />  
   </Property>  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica para anotações de BI para CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
