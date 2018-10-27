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
ms.openlocfilehash: 9a60cce6d752dd6f44c3d94d209557a80cdca863
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147481"
---
# <a name="discoverxeventtracedefinition-rowset"></a>Conjunto de linhas DISCOVER_XEVENT_TRACE_DEFINITION
  Oferece informações sobre os rastreamentos XEvent atualmente ativos no servidor.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas `DISCOVER_XEVENT_TRACE_DEFINITION` contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`Data`|`DBTYPE_WSTR`||A definição XML do rastreamento XEvent.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd1c-8148-11d0-87bb-00c04fc33942|  
|Cadeia de caracteres|DISCOVER_XEVENT_TRACE_DEFINITION|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis Schema Rowsets](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/xml-for-analysis-schema-rowsets)   
 [Usar eventos estendidos do SQL Server &#40;XEvents&#41; monitorar o Analysis Services](../instances/monitor-analysis-services-with-sql-server-extended-events.md)   
 [Usar DMVs &#40;Exibições de Gerenciamento Dinâmico&#41; para monitorar o Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
