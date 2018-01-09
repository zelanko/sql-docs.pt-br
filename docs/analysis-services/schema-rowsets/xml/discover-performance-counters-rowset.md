---
title: Conjunto de linhas DISCOVER_PERFORMANCE_COUNTERS | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 62b1e967-af67-4915-a305-727bffd61fe4
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1d769567a033eedd98eff41aee9cde5306c9b7ea
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="discoverperformancecounters-rowset"></a>Conjunto de linhas DISCOVER_PERFORMANCE_COUNTERS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Retorna o valor de um ou mais contadores de desempenho. Não oferece suporte a contadores que retornam informações sobre uso com o passar do tempo (como leituras de disco por segundo e porcentagem de uso de CPU).  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_PERFORMANCE_COUNTERS** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Restrição|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**PERF_COUNTER_NAME**|**DBTYPE_WSTR**|Obrigatório|O nome do contador de desempenho.|  
|**PERF_COUNTER_VALUE**|**DBTYPE_DOUBLE**||O valor do contador de desempenho.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd2e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PerformanceCounters|  
  
## <a name="see-also"></a>Consulte Também  
 [Conjunto de linhas de esquema do XML](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
