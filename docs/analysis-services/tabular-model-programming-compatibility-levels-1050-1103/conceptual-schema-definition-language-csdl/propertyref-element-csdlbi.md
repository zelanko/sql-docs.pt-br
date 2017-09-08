---
title: Elemento PropertyRef (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
ms.assetid: 8299efb9-e224-4a82-bdfc-a74ec92f8711
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6e2b4e43294d4e5c48500560203e778a21b99724
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="propertyref-element-csdlbi"></a>Elemento PropertyRef (CSDLBI)
  O elemento PropertyRef é um tipo simples que fornece uma referência a uma coluna que fornece um valor exigido por outra propriedade.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento PropertyRef.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|Nome|Sim|Uma cadeia de caracteres que contém o nome da propriedade que é o destino da referência.|  
  
## <a name="propertyrefs-element"></a>Elemento PropertyRefs  
 PropertyRefs é um tipo complexo que define uma coleção de propriedades, em que cada propriedade contida é um elemento PropertyRef.  
  
 A tabela a seguir lista os elementos e atributos do tipo PropertyRefs.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|PropertyRef|Sim|Uma cadeia de caracteres que contém a referência da propriedade.|  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra um elemento PropertyRef que especifica a origem de uma fórmula que é usada em uma medida, no exemplo de modelo de tabela da AdventureWorks.  
  
```  
<bi:Measure Caption="Total Current Quarter Margin Performance" ReferenceName="Total Current Quarter Margin Performance" Width="0" IsSimpleMeasure="false">  
  <bi:Kpi StatusGraphic="Three Symbols UnCircled Colored">  
    <bi:KpiGoal>  
      <bi:PropertyRef Name="Measures___Total_Current_Quarter_Margin_Performance_Goal_" />  
    </bi:KpiGoal>  
    <bi:KpiStatus>  
      <bi:PropertyRef Name="Measures___Total_Current_Quarter_Margin_Performance_Status_" />  
    </bi:KpiStatus>  
  </bi:Kpi>  
</bi:Measure>  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra um KPI do cubo Operações da Contoso. Os elementos PropertyRef apontam para as colunas que contêm a fórmula ou os valores que são usados para definir a meta do KPI e o status relativo à essa meta.  
  
```  
<Property Name="Sum_of_SalesAmount" Type="Decimal" Precision="19" Scale="4">  
   <Documentation>  
     <Summary>KPI Description</Summary>  
   </Documentation>  
     <bi:Measure   
         Caption="Sum of SalesAmount"   
         ReferenceName="Sum of SalesAmount"   
         FormatString="\$#,0.00;(\$#,0.00);\$#,0.00">  
     <bi:Kpi   
           StatusGraphic="Three Circles Colored">  
         <bi:KpiGoal>  
            <bi:PropertyRef Name="v_Sum_of_SalesAmount_Goal" />  
          </bi:KpiGoal>  
          <bi:KpiStatus>  
              <bi:PropertyRef Name="v_Sum_of_SalesAmount_Status" />  
          </bi:KpiStatus>  
     </bi:Kpi>  
     </bi:Measure>  
</Property>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica para anotações de BI para CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
