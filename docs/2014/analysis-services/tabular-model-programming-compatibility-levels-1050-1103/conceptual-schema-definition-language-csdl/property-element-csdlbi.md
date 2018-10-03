---
title: Elemento Property (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: f0770c5e-6420-4d0c-a5bf-b94eaf6877ca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 48442ba8e5d17a652f60aaebb24040345bda474f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055386"
---
# <a name="property-element-csdlbi"></a>Elemento Property (CSDLBI)
  O elemento Property na CSDLBI é um tipo complexo que fornece adições ao elemento CSDL Property, como suporte dos modelos de dados de business intelligence.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento CSDLBI Property.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|Sumário|não|Uma cadeia de caracteres que contém o LCID da solicitação.|  
|DefaultAggregationFunction|Sim|Uma cadeia de caracteres que especifica a função de agregação que deverá ser usada se os cálculos forem executados no atributo e nenhuma outra função tiver sido especificada.<br /><br /> Se não for especificada, será usada a agregação padrão do modelo, que geralmente é SUM.|  
|GroupingBehavior|não|Um valor que especifica como os resultados da consulta são agrupados. O conteúdo do atributo é definido pelo tipo simples TGroupingBehavior (veja a tabela abaixo).|  
|OrderBy|não|Uma referência a outra propriedade dentro do modelo que define a ordem de classificação para os valores da propriedade em questão.<br /><br /> Os valores para as duas propriedades DEVEM ter um mapeamento de um para um. Caso contrário, o comportamento da classificação será indefinida.<br /><br /> Se esse elemento for omitido, as propriedades serão classificadas com base em seus valores.|  
|Stability|não|Um atributo que especifica a estabilidade dos valores da propriedade entre operações de atualização.<br /><br /> Esse atributo não é definido pelos usuários, mas é emitido pelo ambiente no tempo de design apenas para valores instáveis. Ele sempre é aplicado a colunas que contêm um número de linha e a colunas que contêm fórmulas que geram resultados indeterminados, como NOW() ou RAND().<br /><br /> Os valores desse atributo são listados na tabela abaixo, que descreve o tipo simples Stability.|  
  
## <a name="groupingbehavior"></a>GroupingBehavior  
 A tabela a seguir lista os valores do tipo simples GroupingBehavior.  
  
|Valor|Description|  
|-----------|-----------------|  
|GroupOnValue|Agrupe pelo valor do atributo xthe.|  
|GroupOnEntityKey|Agrupe pela chave de entidade.|  
  
 O exemplo a seguir ilustra o uso desses dois valores. Suponha que a consulta foi criada para retornar deduções da folha de pagamento de um determinado usuário, especificado por nome. Supondo que o banco de dados contenha dois usuários com o mesmo nome, mas diferentes identificadores de banco de dados, os resultados da consulta serão diferentes, o que dependerá de qual valor de atributo será aplicado à coluna:  
  
-   `GroupOnValue`: os resultados da consulta incluem as deduções da folha de pagamento de ambos os usuários, totalizadas juntas.  
  
-   `GroupOnEntityKey`: os resultados da consulta incluem as deduções da folha de pagamento de cada usuário, mas listadas individualmente.  
  
## <a name="stability"></a>Stability  
 A tabela a seguir lista os valores do tipo simples `Stability`.  
  
|Valor|Description|  
|-----------|-----------------|  
|Stable|A propriedade permanece constante entre operações de atualização.|  
|RowNumber|A propriedade contém um número de linha.|  
|Volatile|A propriedade pode não permanecer constante entre operações de atualização.|  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
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
 [Referência técnica para Anotações de BI para CSDL](technical-reference-for-bi-annotations-to-csdl.md)  
  
  
