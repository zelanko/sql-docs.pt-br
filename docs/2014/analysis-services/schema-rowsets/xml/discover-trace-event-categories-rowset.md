---
title: Conjunto de linhas DISCOVER_TRACE_EVENT_CATEGORIES | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 1ad74fd2-4740-469d-85b5-abf0171737fd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d5771be15bf30b7cd5d478281ff9d859c354f4d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140146"
---
# <a name="discovertraceeventcategories-rowset"></a>Conjunto de linhas DISCOVER_TRACE_EVENT_CATEGORIES
  Mostra a lista de categorias de evento com suporte no provedor de rastreamento.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_TRACE_EVENT_CATEGORIES` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`Data`|`DBTYPE_WSTR`||Contém uma cadeia de caracteres XML codificada que descreve informações de categoria de evento sobre o provedor de rastreamento, incluindo o nome, o tipo e a descrição da categoria. Type é uma cadeia de caracteres que indica o tipo da categoria de evento. Os valores de enumeração são os seguintes:<br /><br /> -0 = Normal<br />-1 = significativos<br />-2 = erro|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd19-8148-11d0-87bb-00c04fc33942|  
|Cadeia de caracteres|DISCOVER_TRACE_EVENT_CATEGORIES|  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](xml-for-analysis-schema-rowsets.md)  
  
  
