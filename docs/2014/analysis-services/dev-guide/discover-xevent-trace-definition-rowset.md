---
title: Conjunto de linhas DISCOVER_XEVENT_TRACE_DEFINITION | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: e1ce2d2d-f994-4318-801a-ee0385aecd84
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cc223ec3ef09b791772a42134f2c71c73245507a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171206"
---
# <a name="discoverxeventtracedefinition-rowset"></a>Conjunto de linhas DISCOVER_XEVENT_TRACE_DEFINITION
  Oferece informações sobre os rastreamentos XEvent atualmente ativos no servidor.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_XEVENT_TRACE_DEFINITION` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`Data`|`DBTYPE_WSTR`||A definição XML do rastreamento XEvent.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd1c-8148-11d0-87bb-00c04fc33942|  
|Cadeia de caracteres|DISCOVER_XEVENT_TRACE_DEFINITION|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis Schema Rowsets](../schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [Usar eventos estendidos do SQL Server &#40;XEvents&#41; monitorar o Analysis Services](../instances/monitor-analysis-services-with-sql-server-extended-events.md)   
 [Usar exibições de gerenciamento dinâmico &#40;DMVs&#41; monitorar o Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
