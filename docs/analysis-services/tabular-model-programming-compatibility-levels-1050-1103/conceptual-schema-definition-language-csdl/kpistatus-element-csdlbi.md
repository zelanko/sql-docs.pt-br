---
title: Elemento KpiStatus (CSDLBI) | Microsoft Docs
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
ms.assetid: 6fee5b82-caa8-46a1-ad68-bbce3e11e01e
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 574cb8e39b224bcaa5f73be784c0c6aff4d39dde
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="kpistatus-element-csdlbi"></a>Elemento KpiStatus (CSDLBI)
  O elemento KpiStatus define uma referência à coluna que contém o valor usado como o indicador de status em um KPI (Indicador Chave de Desempenho).  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento KpiStatus.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|PropertyRef|Sim|Uma referência a uma coluna que contém o valor usado como o indicador de status em um KPI.<br /><br /> Esse elemento DEVE conter exatamente uma referência de coluna, conforme definido pelo tipo TPropertyRefcomplex.|  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra um KPI do exemplo de modelo de tabela da AdventureWorks. O elemento KpiStatus refere-se a uma coluna (representada como um PropertyRef) que contém o valor.  
  
```  
  
<Property Name="InternetCurrSalesPerf" Type="Double">  
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
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra um KPI do cubo Operações da Contoso. O elemento KpiStatus faz referência a uma medida que calcula o valor do status do KPI.  
  
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
 [Elemento KPI &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)  
  
  

