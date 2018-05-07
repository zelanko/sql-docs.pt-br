---
title: Conjunto de linhas DISCOVER_STORAGE_TABLE_COLUMNS | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6efb37b35d9b2dd521a1848f8ab7ecba7b8f608b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="discoverstoragetablecolumns-rowset"></a>Conjunto de linhas DISCOVER_STORAGE_TABLE_COLUMNS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Fornece informações em nível de coluna sobre tabelas de armazenamento usadas por um banco de dados do Analysis Services executado no modo de Tabela ou SharePoint.  
  
 **Aplica-se a:** modelos tabulares  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **DISCOVER_STORAGE_TABLE_COLUMNS** linhas contém as seguintes colunas.  
  
|**Nome da coluna**|**Indicador de tipo**|**Restrição**|**Descrição**|  
|---------------------|------------------------|---------------------|---------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Sim|Especifica o nome do banco de dados que contém as tabelas. Se ele for omitido, o banco de dados atual será usado.<br /><br /> O **DISCOVER_STORAGE_TABLE_COLUMNS** linhas pode ser restringido usando esta coluna.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Sim|Especifica o cubo ou modelo que contém as tabelas.<br /><br /> É possível restringir o conjunto de linhas **DISCOVER_STORAGE_TABLES** usando esta coluna.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Sim|O nome do grupo de medidas.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||O nome da dimensão.|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||O nome do atributo.|  
|**TABLE_ID**|**DBTYPE_WSTR**||A ID da tabela.|  
|**COLUMN_ID**|**DBTYPE _ WSTR**||A ID da coluna. A ID da coluna é interna ao mecanismo analítico na memória xVelocity (VertiPaq) e é apenas para fins informativos.|  
|**COLUMN_TYPE**|**DBTYPE_WSTR**||O tipo de coluna. O tipo da coluna é interno ao mecanismo analítico na memória xVelocity (VertiPaq) e é apenas para fins informativos.<br /><br /> BASIC_DATA<br /><br /> HIERARCHY_DATAID_TO_POSITION<br /><br /> HIERARCHY_POSITION_TO_DATAID<br /><br /> RELATIONSHIP|  
|**COLUMN_ENCODING**|**DBTYPE_UI8**||Um inteiro que representa o tipo de codificação usado para obter dados de coluna.<br /><br /> **0**, usado com **COLUMN_TYPE**: HIERARCHY_DATAID_TO_POSITION, HIERARCHY_POSITION_TO_DATAID, relação<br /><br /> **1**, usado com **COLUMN_TYPE**: BASIC_DATA<br /><br /> **2**, usado com **COLUMN_TYPE**: BASIC_DATA|  
|**TIPO DE DADOS**|**DBTYPE_WSTR**||O tipo de dados da coluna. Tem os seguintes valores possíveis:<br /><br /> DBTYPE_BOOL<br /><br /> DBTYPE_CY<br /><br /> DBTYPE_DATE<br /><br /> DBTYPE_I4<br /><br /> DBTYPE_I8<br /><br /> DBTYPE_R8<br /><br /> DBTYPE_WSTR<br /><br /> N/A|  
|**ISKEY**|**DBTYPE_BOOL**||**True** se a coluna é usada como uma chave primária ou estrangeira; caso contrário **false**.|  
|**ISUNIQUE**|**DBTYPE_BOOL**||**True** se os valores na coluna forem exclusivos; caso contrário **false**.|  
|**ISNULLABLE**|**DBTYPE_BOOL**||**True** se a coluna for anulável; caso contrário **false**.|  
|**ISROWNUMBER**|**DBTYPE_BOOL**||**True** se a coluna é uma coluna de número de linha. Colunas de número de linha para uso interno pelo mecanismo analítico na memória xVelocity.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
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
 [Conjuntos de linhas do esquema do Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
