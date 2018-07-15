---
title: Conjunto de linhas DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS | Microsoft Docs
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
ms.assetid: 3e514715-9fe6-4e6a-accb-4149ffd7e0bf
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ae9955e9f052e4be2317206d5618ccf9294232cb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325016"
---
# <a name="discoverstoragetablecolumnsegments-rowset"></a>Conjunto de linhas DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS
  Fornece informações em nível de coluna e segmento sobre tabelas de armazenamento usadas por um banco de dados do Analysis Services executado no modo tabular ou do PowerPivot. Este conjunto de linhas é usado principalmente para solução e análise de problemas.  
  
 **Aplica-se a:** modelos tabulares  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS` linhas contém as colunas a seguir.  
  
|**Nome da coluna**|**Indicador de tipo**|**Restrição**|**Descrição**|  
|---------------------|------------------------|---------------------|---------------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Sim|Especifica o banco de dados tabular.<br /><br /> O `DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS` conjunto de linhas pode ser restrito usando esta coluna. Se ele for omitido, o banco de dados atual será usado.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Sim|O nome do modelo.<br /><br /> O `DISCOVER_STORAGE_TABLES` conjunto de linhas pode ser restrito usando esta coluna.|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|Sim|O nome do grupo de medidas.|  
|`PARTITION_NAME`|`DBTYPE_WSTR`|Sim|O nome da partição.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||O nome da dimensão.|  
|`TABLE_ID`|`DBTYPE_WSTR`||A ID interna do segmento de tabela.|  
|`COLUMN_ID`|`DBTYPE_WSTR`||A ID interna da coluna.|  
|`SEGMENT _NUMBER`|`DBTYPE_I8`||O número ordinal do segmento de tabela.|  
|`TABLE_PARTTION_NUMBER`|`DBTYPE_I8`||O número ordinal da partição.|  
|`RECORDS_COUNT`|`DBTYPE_I8`||O número de registros na partição.|  
|`ALLOCATED_SIZE`|`DBTYPE_UI8`||Tamanho em bytes alocado ao segmento de coluna.|  
|`USED_SIZE`|`DBTYPE_UI8`||Tamanho em bytes usado pelo segmento de coluna.|  
|`COMPRESSION_TYPE`|`DBTYPE_WSTR`||Tipo de compactação aplicado ao segmento de coluna. Este valor destina-se somente ao uso interno e para fins de suporte ao cliente. A Microsoft não publica valores ou descrições válidos para esta coluna.|  
|`BITS_COUNT`|`DBTYPE_I8`||A contagem de bits.|  
|`BOOKMARK_BITS_COUNT`|`DBTYPE_I8`||A contagem de bits de indicador.|  
|`VERTIPAQ_STATE`|`DBTYPE_WSTR`||O estado da compactação de VertiPaq para este segmento de coluna. O valor é um dos seguintes:<br /><br /> -SKIPPED – a compactação de VertiPaq foi ignorada.<br />-CONCLUÍDA – a compactação de VertiPaq foi concluída com êxito.<br />Compactação de - TIMEBOXED – o VertiPaq foi definida em timebox.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd45-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|StorageSegments|  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir retorna os segmentos de tabela de armazenamento associados com o atributo modelo LastName, no banco de dados atual.  
  
```  
SELECT DISTINCT TABLE_ID, COLUMN_ID   
FROM $system.DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS  
WHERE COLUMN_ID = 'LastName'  
ORDER BY TABLE_ID  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema do Analysis Services](../analysis-services-schema-rowsets.md)  
  
  
