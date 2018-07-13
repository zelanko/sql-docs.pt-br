---
title: Conjunto de linhas DISCOVER_STORAGE_TABLE_COLUMNS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 24abb88e-33a9-4ae2-829d-cdef0ff22ec1
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e480f60aa857506a1d192452b299cede3f7161e5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153147"
---
# <a name="discoverstoragetablecolumns-rowset"></a>Conjunto de linhas DISCOVER_STORAGE_TABLE_COLUMNS
  Fornece informações em nível de coluna sobre tabelas de armazenamento usadas por um banco de dados do Analysis Services executado no modo de Tabela ou SharePoint.  
  
 **Aplica-se a:** modelos tabulares  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_STORAGE_TABLE_COLUMNS` linhas contém as colunas a seguir.  
  
|**Nome da coluna**|**Indicador de tipo**|**Restrição**|**Descrição**|  
|---------------------|------------------------|---------------------|---------------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Sim|Especifica o nome do banco de dados que contém as tabelas. Se ele for omitido, o banco de dados atual será usado.<br /><br /> O `DISCOVER_STORAGE_TABLE_COLUMNS` conjunto de linhas pode ser restrito usando esta coluna.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Sim|Especifica o cubo ou modelo que contém as tabelas.<br /><br /> O `DISCOVER_STORAGE_TABLES` conjunto de linhas pode ser restrito usando esta coluna.|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|Sim|O nome do grupo de medidas.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||O nome da dimensão.|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||O nome do atributo.|  
|`TABLE_ID`|`DBTYPE_WSTR`||A ID da tabela.|  
|`COLUMN_ID`|`DBTYPE_ WSTR`||A ID da coluna. A ID da coluna é interna ao mecanismo analítico na memória xVelocity (VertiPaq) e é apenas para fins informativos.|  
|`COLUMN_TYPE`|`DBTYPE_WSTR`||O tipo de coluna. O tipo da coluna é interno ao mecanismo analítico na memória xVelocity (VertiPaq) e é apenas para fins informativos.<br /><br /> -BASIC_DATA<br />-HIERARCHY_DATAID_TO_POSITION<br />-HIERARCHY_POSITION_TO_DATAID<br />-A RELAÇÃO|  
|`COLUMN_ENCODING`|`DBTYPE_UI8`||Um inteiro que representa o tipo de codificação usado para obter dados de coluna.<br /><br /> -   **0**, usado com `COLUMN_TYPE`: HIERARCHY_DATAID_TO_POSITION, HIERARCHY_POSITION_TO_DATAID, relação<br />-   **1**, usado com `COLUMN_TYPE`: BASIC_DATA<br />-   **2**, usado com `COLUMN_TYPE`: BASIC_DATA|  
|`DATATYPE`|`DBTYPE_WSTR`||O tipo de dados da coluna. Tem os seguintes valores possíveis:<br /><br /> -DBTYPE_BOOL<br />-DBTYPE_CY<br />-DBTYPE_DATE<br />-DBTYPE_I4<br />-DBTYPE_I8<br />-DBTYPE_R8<br />-DBTYPE_WSTR<br />-N/D|  
|`ISKEY`|`DBTYPE_BOOL`||`True` se a coluna for usada como uma chave primária ou estrangeira; caso contrário, `false`.|  
|`ISUNIQUE`|`DBTYPE_BOOL`||`True` se os valores na coluna forem exclusivos; caso contrário, `false`.|  
|`ISNULLABLE`|`DBTYPE_BOOL`||`True` se a coluna for anulável; caso contrário, `false`.|  
|`ISROWNUMBER`|`DBTYPE_BOOL`||`True` se a coluna for uma coluna de número de linha. Colunas de número de linha para uso interno pelo mecanismo analítico na memória xVelocity.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd44-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|StorageTableColumns|  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir usa uma consulta DMV para retornar o conjunto de resultados.  
  
```  
SELECT *  
FROM $System.DISCOVER_STORAGE_TABLE_COLUMNS  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema do Analysis Services](../analysis-services-schema-rowsets.md)  
  
  
