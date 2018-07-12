---
title: Elemento KpiGoal (CSDLBI) | Microsoft Docs
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
ms.assetid: fd8afbe7-b57d-4b47-862d-eb7b2489c327
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b64e3124ba7a848921e1b0844b20d03e9aa82af4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165237"
---
# <a name="kpigoal-element-csdlbi"></a>Elemento KpiGoal (CSDLBI)
  O elemento KpiGoal fornece uma referência à coluna que é usada para definir a meta do KPI (Indicador Chave de Desempenho).  
  
 Em um CSDLBI, os KPIs se baseiam em medidas e o elemento Measure contém a fórmula (se houver), enquanto outros metadados associados ao KPI são definidos como parte do [elemento KPI &#40;CSDLBI&#41;](kpi-element-csdlbi.md).  O elemento Kpigoal é um subtipo do elemento Kpi.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os atributos que definem o elemento KpiGoal.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|PropertyRef|Sim|Uma referência à coluna que contém o valor de meta do KPI.<br /><br /> O elemento Kpigoal deve conter exatamente um elemento PropertyRef.<br /><br /> Consulte [PropertyRef Element &#40;CSDLBI&#41;](propertyref-element-csdlbi.md).|  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra um KPI do modelo de exemplo da AdventureWorks.  
  
```  
  
<Property Name="InternetCurrentSalesPerformance" Type="Double">  
  <bi:Measure>  
    <bi:Kpi StatusGraphic="Three Stars Colored">  
      <bi:KpiGoal>  
        <bi:PropertyRef Name="v_InternetCurrSalesPerf_Goal" />  
      </bi:KpiGoal>  
      <bi:KpiStatus>  
        <bi:PropertyRef Name="v_InternetCurrSalesPerf_Status" />  
      </bi:KpiStatus>  
    </bi:Kpi>  
  </bi:Measure>  
</Property>  
  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra um KPI do cubo Operações da Contoso.  
  
```  
<bi:Measure   
       Caption="Sum of SalesAmount"   
       ReferenceName="Sum of SalesAmount"   
       FormatString="\$#,0.00;(\$#,0.00);\$#,0.00">  
    <bi:Kpi   
       StatusGraphic="Three Circles Colored">  
      <bi:KpiGoal>  
         <bi:PropertyRef   
          Name="v_Sum_of_SalesAmount_Goal" />  
       </bi:KpiGoal>  
       <bi:KpiStatus>  
          <bi:PropertyRef   
          Name="v_Sum_of_SalesAmount_Status" />  
        </bi:KpiStatus>  
       </bi:Kpi>  
</bi:Measure>  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Elemento KPI &#40;CSDLBI&#41;](kpi-element-csdlbi.md)  
  
  
