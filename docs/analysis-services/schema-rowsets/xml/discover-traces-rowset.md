---
title: Conjunto de linhas DISCOVER_TRACES | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 63bcb03d27abdacf675acd56c95a2dbd49adb362
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="discovertraces-rowset"></a>Conjunto de linhas DISCOVER_TRACES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Oferece informações sobre os rastreamentos atualmente ativos no servidor.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_TRACES** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**TraceID**|**DBTYPE_WSTR**|A ID de rastreamento.|  
|**traceName**|**DBTYPE_WSTR**|O nome do rastreamento.|  
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
|Cadeia de caracteres|DISCOVER_TRACES|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
