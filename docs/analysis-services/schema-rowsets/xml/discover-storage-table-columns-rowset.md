---
title: Conjunto de linhas DISCOVER_STORAGE_TABLE_COLUMNS | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
ms.assetid: 24abb88e-33a9-4ae2-829d-cdef0ff22ec1
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 126a0f1c261cc13f5a3673a67c87d12aac5faece
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="discoverstoragetablecolumns-rowset"></a>Conjunto de linhas DISCOVER_STORAGE_TABLE_COLUMNS
  Fornece informações em nível de coluna sobre tabelas de armazenamento usadas por um banco de dados do Analysis Services executado no modo de Tabela ou SharePoint.  
  
 **Aplica-se a:** modelos tabulares  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **DISCOVER_STORAGE_TABLE_COLUMNS** linhas contém as seguintes colunas.  
  
|**Nome da coluna**|**Indicador de tipo**|**Restrição**|**Description**|  
|---------------------|------------------------|---------------------|---------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Sim|Especifica o nome do banco de dados que contém as tabelas. Se ele for omitido, o banco de dados atual será usado.<br /><br /> O **DISCOVER_STORAGE_TABLE_COLUMNS** linhas pode ser restringido usando esta coluna.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Sim|Especifica o cubo ou modelo que contém as tabelas.<br /><br /> É possível restringir o conjunto de linhas **DISCOVER_STORAGE_TABLES** usando esta coluna.|  
|**NOME_GRUPO_MEDIDAS**|**DBTYPE_WSTR**|Sim|O nome do grupo de medidas.|  
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
 [Conjuntos de linhas de esquema do Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
