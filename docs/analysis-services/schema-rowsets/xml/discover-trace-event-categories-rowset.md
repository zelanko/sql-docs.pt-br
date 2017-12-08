---
title: Conjunto de linhas DISCOVER_TRACE_EVENT_CATEGORIES | Microsoft Docs
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
ms.assetid: 1ad74fd2-4740-469d-85b5-abf0171737fd
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 64e00a56cac41e46ba7427f17d4f0471ff7724ac
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="discovertraceeventcategories-rowset"></a>Conjunto de linhas DISCOVER_TRACE_EVENT_CATEGORIES
  Mostra a lista de categorias de evento com suporte no provedor de rastreamento.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_TRACE_EVENT_CATEGORIES** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**Dados**|**DBTYPE_WSTR**||Contém uma cadeia de caracteres XML codificada que descreve informações de categoria de evento sobre o provedor de rastreamento, incluindo o nome, o tipo e a descrição da categoria. Type é uma cadeia de caracteres que indica o tipo da categoria de evento. Os valores de enumeração são os seguintes:<br /><br /> 0=Normal<br /><br /> 1=Significativo<br /><br /> 2=Erro|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd19-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRACE_EVENT_CATEGORIES|  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
