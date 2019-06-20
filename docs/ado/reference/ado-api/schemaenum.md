---
title: SchemaEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SchemaEnum
helpviewer_keywords:
- SchemaEnum enumeration [ADO]
ms.assetid: 21c97651-297f-469f-b5b5-c48af72b62a8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4aa145a3c42c5ed807a63dc551e67afe6af95cde
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711307"
---
# <a name="schemaenum"></a>SchemaEnum
Especifica o tipo de esquema **conjunto de registros** que o [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) recupera do método.  
  
## <a name="remarks"></a>Comentários  
 Informações adicionais sobre a função e colunas retornadas para cada constante do ADO pode ser encontrada nos tópicos [apêndice b: Conjuntos de linhas de esquema](https://msdn.microsoft.com/2b5fbf03-e50d-44ee-bc57-5a57666c55f1) de referência do programador do OLE DB. O nome de cada tópico é listado entre parênteses na seção de descrição da tabela a seguir.  
  
 Informações adicionais sobre a função e colunas retornadas para cada constante do ADO MD pode ser encontrada nos tópicos [OLE DB para objetos OLAP e conjuntos de linhas de esquema](https://msdn.microsoft.com/d20bb2a6-68bd-423f-9ec8-eb930cd0c144) no OLE DB para a documentação Online Analytical Processing (OLAP). O nome de cada tópico é listado entre parênteses na coluna Descrição da tabela a seguir.  
  
 Você pode converter os tipos de dados das colunas na documentação do OLE DB para tipos de dados ADO referindo-se a coluna Description do ADO [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) tópico. Por exemplo, um tipo de dados OLE DB do **DBTYPE_WSTR** é equivalente a um tipo de dados do ADO **adWChar**.  
  
 O ADO gera resultados semelhantes de esquema para as constantes **adSchemaDBInfoKeywords** e **adSchemaDBInfoLiterals**. ADO cria uma **conjunto de registros**e, em seguida, preenche cada linha com os valores retornados, respectivamente o **IDBInfo::GetKeywords** e **IDBInfo::GetLiteralInfo** métodos. Informações adicionais sobre esses métodos podem ser encontradas na [IDBInfo](https://msdn.microsoft.com/3f5ad97f-3fc6-4f21-b691-f6911e4007f3) seção da referência do OLE DB do programador.  
  
|Constante|Valor|Descrição|Colunas de restrição|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|Retorna as asserções definidas no catálogo e pertencentes a um determinado usuário.<br /><br /> (As declarações do conjunto de linhas)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|Retorna os atributos físicos associados a catálogos acessíveis a partir do DBMS.<br /><br /> (CATÁLOGOS do conjunto de linhas)|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|Retorna os conjuntos de caracteres definidos no catálogo acessíveis para um determinado usuário.<br /><br /> (Conjunto de linhas CHARACTER_SETS)|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|Retorna as restrições de verificação definidas no catálogo e pertencentes a um determinado usuário.<br /><br /> (CHECK_CONSTRAINTS) Conjunto de linhas)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|Retorna os agrupamentos de caracteres definidos no catálogo acessíveis para um determinado usuário.<br /><br /> (Conjunto de linhas de AGRUPAMENTOS)|COLLATION_CATALOG COLLATION_SCHEMA COLLATION_NAME|  
|**adSchemaColumnPrivileges**|13|Retorna os privilégios em colunas de tabelas definidas no catálogo que estão disponíveis ou foram concedidas por um determinado usuário.<br /><br /> (Conjunto de linhas COLUMN_PRIVILEGES)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|**adSchemaColumns**|4|Retorna as colunas de tabelas (incluindo exibições) definidas no catálogo que são acessíveis para um determinado usuário.<br /><br /> (Colunas do conjunto de linhas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|Retorna as colunas definidas no catálogo que são dependentes de um domínio definido no catálogo e pertencentes a um determinado usuário.<br /><br /> (Conjunto de linhas COLUMN_DOMAIN_USAGE)|DOMAIN_CATALOG DOMAIN_SCHEMA DOMAIN_NAME COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|Retorna as colunas usadas por restrições referenciais, restrições exclusivas, restrições de verificação e asserções definidas no catálogo e pertencentes a um determinado usuário.<br /><br /> (CONSTRAINT_COLUMN_USAGE Rowset)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|Retorna as tabelas que são usadas por restrições referenciais, restrições exclusivas, restrições de verificação e asserções definidas no catálogo e pertencentes a um determinado usuário.<br /><br /> (CONSTRAINT_TABLE_USAGE Rowset)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaCubes**|32|Retorna informações sobre os cubos disponíveis em um esquema (ou do catálogo, se o provedor não dá suporte a esquemas).<br /><br /> (Conjunto de linhas de CUBOS *)|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|Retorna uma lista de palavras-chave específicas do provedor.<br /><br /> (IDBInfo::GetKeywords)|\<Nenhum >|  
|**adSchemaDBInfoLiterals**|31|Retorna uma lista de literais específicas do provedor usada nos comandos de texto.<br /><br /> (IDBInfo::GetLiteralInfo)|\<Nenhum >|  
|**adSchemaDimensions**|33|Retorna informações sobre as dimensões em um determinado cubo. Ele tem uma linha para cada dimensão.<br /><br /> (Conjunto de linhas de dimensões)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|Retorna as colunas de chave estrangeiras definidas no catálogo por um determinado usuário.<br /><br /> (Conjunto de linhas FOREIGN_KEYS)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|Retorna informações sobre as hierarquias disponíveis em uma dimensão.<br /><br /> (Conjunto de linhas de HIERARQUIAS)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|Retorna os índices definidos no catálogo e pertencentes a um determinado usuário.<br /><br /> (Conjunto de linhas de ÍNDICES)|TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TYPE TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|Retorna as colunas definidas no catálogo que são restringidas como chaves por um determinado usuário.<br /><br /> (KEY_COLUMN_USAGE Rowset)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaLevels**|35|Retorna informações sobre os níveis disponíveis em uma dimensão.<br /><br /> (Os níveis do conjunto de linhas)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_NAME LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|Retorna informações sobre as medidas disponíveis.<br /><br /> (Conjunto de linhas de medidas)|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|Retorna informações sobre os membros disponíveis.<br /><br /> (Os MEMBROS do conjunto de linhas)|Operador CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE árvore. Para obter mais informações, consulte o OLE DB para Online Analytical Processing (OLAP).|  
|**adSchemaPrimaryKeys**|28|Retorna as colunas de chave primárias definidas no catálogo por um determinado usuário.<br /><br /> (Conjunto de linhas PRIMARY_KEYS)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|Retorna informações sobre as colunas de conjuntos de linhas retornadas por procedimentos.<br /><br /> (PROCEDURE_COLUMNS Rowset)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|Retorna informações sobre os parâmetros e códigos de retorno de procedimentos.<br /><br /> (Conjunto de linhas PROCEDURE_PARAMETERS)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|**adSchemaProcedures**|16|Retorna os procedimentos definidos no catálogo e pertencentes a um determinado usuário.<br /><br /> (Conjunto de linhas de procedimentos)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|Retorna informações sobre as propriedades disponíveis para cada nível da dimensão.<br /><br /> (Propriedades do conjunto de linhas)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|Usado se o provedor define suas próprias consultas de esquema não padrão.|\<Específico do provedor >|  
|**adSchemaProviderTypes**|22|Retorna os tipos de dados (base) suportados pelo provedor de dados.<br /><br /> (Conjunto de linhas PROVIDER_TYPES)|DATA_TYPE BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|Retorna as restrições referenciais definidas no catálogo e pertencentes a um determinado usuário.<br /><br /> (REFERENTIAL_CONSTRAINTS Rowset)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|Retorna os esquemas (objetos de banco de dados) que pertencem a um determinado usuário.<br /><br /> (Conjunto de linhas de esquema)|CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|Retorna os níveis de conformidade, opções e dialetos com suporte nos dados de processamento de implementação de SQL definidos no catálogo.<br /><br /> (SQL_LANGUAGES Rowset)|\<Nenhum >|  
|**adSchemaStatistics**|19|Retorna as estatísticas definidas no catálogo e pertencentes a um determinado usuário.<br /><br /> (Conjunto de linhas de estatísticas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaTableConstraints**|10|Retorna as restrições de tabela definidas no catálogo e pertencentes a um determinado usuário.<br /><br /> (Conjunto de linhas TABLE_CONSTRAINTS)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|Retorna os privilégios em tabelas definidas no catálogo que estão disponíveis ou foram concedidas por um determinado usuário.<br /><br /> (Conjunto de linhas TABLE_PRIVILEGES)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|**adSchemaTables**|20|Retorna as tabelas (incluindo exibições) definidas no catálogo acessíveis para um determinado usuário.<br /><br /> (Conjunto de linhas de tabelas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|**adSchemaTranslations**|21|Retorna as conversões de caracteres definidas no catálogo acessíveis para um determinado usuário.<br /><br /> (Conjunto de linhas de traduções)|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|39|Reservado para uso futuro.||  
|**adSchemaUsagePrivileges**|15|Retorna os privilégios USAGE nos objetos definidos no catálogo que estão disponíveis ou foram concedidas por um determinado usuário.<br /><br /> (Conjunto de linhas USAGE_PRIVILEGES)|OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME OBJECT_TYPE GRANTOR GRANTEE|  
|**adSchemaViewColumnUsage**|24|Retorna as colunas nas quais tabelas exibidas, definidas no catálogo e pertencem a um determinado usuário, são dependentes.<br /><br /> (VIEW_COLUMN_USAGE Rowset)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|Retorna as exibições definidas no catálogo acessíveis para um determinado usuário.<br /><br /> (Modos de exibição do conjunto de linhas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaViewTableUsage**|25|Retorna as tabelas em que tabelas exibidas, definidas no catálogo e pertencem a um determinado usuário, são dependentes.<br /><br /> (Conjunto de linhas VIEW_TABLE_USAGE)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.Schema.ASSERTS|  
|AdoEnums.Schema.CATALOGS|  
|AdoEnums.Schema.CHARACTERSETS|  
|AdoEnums.Schema.CHECKCONSTRAINTS|  
|AdoEnums.Schema.COLLATIONS|  
|AdoEnums.Schema.COLUMNPRIVILEGES|  
|AdoEnums.Schema.COLUMNS|  
|AdoEnums.Schema.COLUMNSDOMAINUSAGE|  
|AdoEnums.Schema.CONSTRAINTCOLUMNUSAGE|  
|AdoEnums.Schema.CONSTRAINTTABLEUSAGE|  
|AdoEnums.Schema.CUBES|  
|AdoEnums.Schema.DBINFOKEYWORDS|  
|AdoEnums.Schema.DBINFOLITERALS|  
|AdoEnums.Schema.DIMENSIONS|  
|AdoEnums.Schema.FOREIGNKEYS|  
|AdoEnums.Schema.HIERARCHIES|  
|AdoEnums.Schema.INDEXES|  
|AdoEnums.Schema.KEYCOLUMNUSAGE|  
|AdoEnums.Schema.LEVELS|  
|AdoEnums.Schema.MEASURES|  
|AdoEnums.Schema.MEMBERS|  
|AdoEnums.Schema.PRIMARYKEYS|  
|AdoEnums.Schema.PROCEDURECOLUMNS|  
|AdoEnums.Schema.PROCEDUREPARAMETERS|  
|AdoEnums.Schema.PROCEDURES|  
|AdoEnums.Schema.PROPERTIES|  
|AdoEnums.Schema.PROVIDERSPECIFIC|  
|AdoEnums.Schema.PROVIDERTYPES|  
|AdoEnums.Schema.REFERENTIALCONTRAINTS|  
|AdoEnums.Schema.SCHEMATA|  
|AdoEnums.Schema.SQLLANGUAGES|  
|AdoEnums.Schema.STATISTICS|  
|AdoEnums.Schema.TABLECONSTRAINTS|  
|AdoEnums.Schema.TABLEPRIVILEGES|  
|AdoEnums.Schema.TABLES|  
|AdoEnums.Schema.TRANSLATIONS|  
|AdoEnums.Schema.TRUSTEES|  
|AdoEnums.Schema.USAGEPRIVILEGES|  
|AdoEnums.Schema.VIEWCOLUMNUSAGE|  
|AdoEnums.Schema.VIEWS|  
|AdoEnums.Schema.VIEWTABLEUSAGE|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
