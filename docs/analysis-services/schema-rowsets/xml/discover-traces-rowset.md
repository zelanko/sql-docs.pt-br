---
title: Conjunto de linhas DISCOVER_TRACES | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 1be6a035-ffc9-489e-9d4d-7391b3e384e2
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b48a6756325dc95da634842c5f695378b20319b9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="discovertraces-rowset"></a>Conjunto de linhas DISCOVER_TRACES
  Oferece informações sobre os rastreamentos atualmente ativos no servidor.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_TRACES** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**TraceID**|**DBTYPE_WSTR**|A ID de rastreamento.|  
|**TraceName**|**DBTYPE_WSTR**|O nome do rastreamento.|  
|**LogFileName**|**DBTYPE_WSTR**|O nome do arquivo de log de rastreamento.|  
|**LogFileSize**|**DBTYPE_I4**|O tamanho do arquivo de log de rastreamento.|  
|**LogFileRollover**|**DBTYPE_BOOL**|Quando o valor for true, indicará que o arquivo de log deve ser substituído; caso contrário, será false.|  
|**Reinicialização automática**|**DBTYPE_BOOL**|Quando o valor for true, indicará que a opção de reinicialização automática está habilitada; caso contrário, será false.|  
|**CreationTime**|**DBTYPE_TIME**|A data e a hora em que o rastreamento foi criado.|  
|**StopTime**|**DBTYPE_TIME**|A hora de parada de um rastreamento.|  
|**Tipo**|**PF_DBTYPE_WSTR**|O tipo de rastreamento.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DISCOVER_TRACES** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**TraceId**|**DBTYPE_I4**|Opcional.|  
|**Tipo**|WSTR|Opcional.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd1a-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRACES|  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
