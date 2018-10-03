---
title: Conjunto de linhas DISCOVER_DIMENSION_STAT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 639f8cd7-3b43-40d5-8b84-552daf60d484
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 39ae0bed8c0e0ff7eb272062b79b870dfb31157e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094976"
---
# <a name="discoverdimensionstat-rowset"></a>Conjunto de linhas DISCOVER_DIMENSION_STAT
  Fornece informações sobre uma dimensão, inclusive o nome do banco de dados que a contém, o nome da dimensão, seus atributos e uma contagem dos membros de cada atributo. Em um modelo de tabela, isso corresponde às colunas em uma tabela e ao número de valores em cada coluna.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_DIMENSION_STAT` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Restrição|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Obrigatório|O nome do banco de dados que contém a dimensão.<br /><br /> Esta coluna é obrigatória na lista de restrições.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`|Obrigatório|O nome da dimensão.<br /><br /> Esta coluna é obrigatória na lista de restrições.|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||O atributo de um atributo na dimensão.|  
|`ATTRIBUTE_COUNT`|`DBTYPE_I8`||A contagem de valores no atributo nomeado. Para um modelo de tabela, o valor sempre equivale ao número de linhas na tabela.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd90-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](xml-for-analysis-schema-rowsets.md)  
  
  
