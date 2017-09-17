---
title: SchemaEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- SchemaEnum
helpviewer_keywords:
- SchemaEnum enumeration [ADO]
ms.assetid: 21c97651-297f-469f-b5b5-c48af72b62a8
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b0b17893425ea772c848b9fb20907c4e0899d1e3
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="schemaenum"></a>SchemaEnum
Especifica o tipo de esquema **registros** que o [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) recupera do método.  
  
## <a name="remarks"></a>Comentários  
 Informações adicionais sobre a função e colunas retornadas para cada constante ADO pode ser encontrada nos tópicos [apêndice b: Schema Rowsets](http://msdn.microsoft.com/en-us/2b5fbf03-e50d-44ee-bc57-5a57666c55f1) de referência OLE DB do programador. O nome de cada tópico está listado entre parênteses na seção de descrição da tabela a seguir.  
  
 Informações adicionais sobre a função e colunas retornadas para cada constante ADO MD pode ser encontrada nos tópicos [OLE DB para conjuntos de linhas de esquema e objetos OLAP](http://msdn.microsoft.com/en-us/d20bb2a6-68bd-423f-9ec8-eb930cd0c144) no OLE DB para a documentação de processamento analítico Online (OLAP). O nome de cada tópico está listado entre parênteses na coluna Descrição da tabela a seguir.  
  
 Você pode converter os tipos de dados das colunas na documentação do OLE DB para tipos de dados ADO referindo-se a coluna de descrição de ADO [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) tópico. Por exemplo, um tipo de dados OLE DB de **DBTYPE_WSTR** é equivalente a um tipo de dados ADO do **adWChar**.  
  
 ADO gera resultados semelhantes de esquema para as constantes, **adSchemaDBInfoKeywords** e **adSchemaDBInfoLiterals**. ADO cria um **registros**e, em seguida, preenche cada linha com os valores retornados respectivamente o **IDBInfo::GetKeywords** e **IDBInfo::GetLiteralInfo** métodos. Informações adicionais sobre esses métodos podem ser encontradas no [IDBInfo](http://msdn.microsoft.com/en-us/3f5ad97f-3fc6-4f21-b691-f6911e4007f3) seção da referência do OLE DB do programador.  
  
|Constante|Valor|Description|Colunas de restrição|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|Retorna as asserções definidas no catálogo que são de propriedade de um determinado usuário.<br /><br /> (Conjunto de linhas de ASSERÇÕES)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|Retorna os atributos físicos associados a catálogos acessíveis a partir do DBMS.<br /><br /> (CATÁLOGOS do conjunto de linhas)|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|Retorna os conjuntos de caracteres definidos no catálogo e acessíveis para um determinado usuário.<br /><br /> (Conjunto de linhas CHARACTER_SETS)|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|Retorna as restrições de verificação definidas no catálogo que são de propriedade de um determinado usuário.<br /><br /> (CHECK_CONSTRAINTS) Conjunto de linhas)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|Retorna os agrupamentos de caracteres definidos no catálogo e acessíveis para um determinado usuário.<br /><br /> (Conjunto de linhas de AGRUPAMENTOS)|COLLATION_CATALOG COLLATION_SCHEMA COLLATION_NAME|  
|**adSchemaColumnPrivileges**|13|Retorna os privilégios em colunas de tabelas definidas no catálogo que estão disponíveis para ou concedido por um determinado usuário.<br /><br /> (Conjunto de linhas COLUMN_PRIVILEGES)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|**adSchemaColumns**|4|Retorna as colunas de tabelas (incluindo exibições) definidas no catálogo que são acessíveis para um determinado usuário.<br /><br /> (Conjunto de linhas de colunas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|Retorna as colunas definidas no catálogo dependentes em um domínio definidas no catálogo e pertencentes a um determinado usuário.<br /><br /> (Conjunto de linhas COLUMN_DOMAIN_USAGE)|DOMAIN_CATALOG DOMAIN_SCHEMA DOMAIN_NAME COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|Retorna as colunas usadas por restrições referenciais, restrições exclusivas, restrições de verificação e asserções definidas no catálogo e pertencentes a um determinado usuário.<br /><br /> (Conjunto de linhas CONSTRAINT_COLUMN_USAGE)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|Retorna as tabelas que são usadas por restrições referenciais, restrições exclusivas, restrições de verificação e asserções definidas no catálogo e pertencentes a um determinado usuário.<br /><br /> (Conjunto de linhas CONSTRAINT_TABLE_USAGE)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaCubes**|32|Retorna informações sobre os cubos disponíveis em um esquema (ou o catálogo, se o provedor não dá suporte a esquemas).<br /><br /> (Linhas CUBOS *)|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|Retorna uma lista de palavras-chave específicas do provedor.<br /><br /> (IDBInfo::GetKeywords)|\<Nenhum >|  
|**adSchemaDBInfoLiterals**|31|Retorna uma lista de literais específico do provedor em comandos de texto.<br /><br /> (IDBInfo::GetLiteralInfo)|\<Nenhum >|  
|**adSchemaDimensions**|33|Retorna informações sobre as dimensões em um determinado cubo. Ele tem uma linha para cada dimensão.<br /><br /> (Conjunto de linhas de dimensões)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|Retorna as colunas de chave estrangeiras definidas no catálogo por um determinado usuário.<br /><br /> (Conjunto de linhas FOREIGN_KEYS)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|Retorna informações sobre as hierarquias disponíveis em uma dimensão.<br /><br /> (Conjunto de linhas de HIERARQUIAS)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|Retorna os índices definidos no catálogo que são de propriedade de um determinado usuário.<br /><br /> (Conjunto de linhas de ÍNDICES)|TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TIPO TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|Retorna as colunas definidas no catálogo que são restringidas como chaves de um determinado usuário.<br /><br /> (Conjunto de linhas KEY_COLUMN_USAGE)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaLevels**|35|Retorna informações sobre os níveis disponíveis em uma dimensão.<br /><br /> (Os níveis do conjunto de linhas)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_NAME LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|Retorna informações sobre as medidas disponíveis.<br /><br /> (Conjunto de linhas de medidas)|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|Retorna informações sobre os membros disponíveis.<br /><br /> (Os MEMBROS do conjunto de linhas)|Operador de CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE árvore. Para obter mais informações, consulte o OLE DB para OLAP processamento analítico Online ().|  
|**adSchemaPrimaryKeys**|28|Retorna as colunas de chave primária definidas no catálogo por um determinado usuário.<br /><br /> (Conjunto de linhas PRIMARY_KEYS)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|Retorna informações sobre as colunas de conjuntos de linhas retornadas por procedimentos.<br /><br /> (Conjunto de linhas PROCEDURE_COLUMNS)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|Retorna informações sobre os parâmetros e códigos de retorno de procedimentos.<br /><br /> (Conjunto de linhas PROCEDURE_PARAMETERS)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|**adSchemaProcedures**|16|Retorna os procedimentos definidos no catálogo que são de propriedade de um determinado usuário.<br /><br /> (Conjunto de linhas de procedimentos)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|Retorna informações sobre as propriedades disponíveis para cada nível da dimensão.<br /><br /> (Propriedades do conjunto de linhas)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|Usado se o provedor define suas próprias consultas de esquema padrão.|\<Específico do provedor >|  
|**adSchemaProviderTypes**|22|Retorna os tipos de dados (base) suportados pelo provedor de dados.<br /><br /> (Linhas PROVIDER_TYPES)|DATA_TYPE BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|Retorna as restrições referenciais definidas no catálogo que são de propriedade de um determinado usuário.<br /><br /> (Conjunto de linhas REFERENTIAL_CONSTRAINTS)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|Retorna os esquemas (objetos de banco de dados) que são de propriedade de um determinado usuário.<br /><br /> (Conjunto de linhas de esquema)|CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|Retorna os níveis de conformidade, opções e dialetos suportados pelo banco de dados de processamento de implementação de SQL definidos no catálogo.<br /><br /> (Conjunto de linhas SQL_LANGUAGES)|\<Nenhum >|  
|**adSchemaStatistics**|19|Retorna as estatísticas definidas no catálogo que são de propriedade de um determinado usuário.<br /><br /> (Conjunto de linhas de estatísticas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaTableConstraints**|10|Retorna as restrições de tabela definidas no catálogo que são de propriedade de um determinado usuário.<br /><br /> (Conjunto de linhas TABLE_CONSTRAINTS)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|Retorna os privilégios em tabelas definidas no catálogo que estão disponíveis para ou concedido por um determinado usuário.<br /><br /> (Conjunto de linhas TABLE_PRIVILEGES)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|**adSchemaTables**|20|Retorna as tabelas (incluindo exibições) definidas no catálogo que são acessíveis para um determinado usuário.<br /><br /> (Conjunto de linhas de tabelas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|**adSchemaTranslations**|21|Retorna as traduções de caracteres definidas no catálogo e acessíveis para um determinado usuário.<br /><br /> (Conjunto de linhas de traduções)|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|39|Reservado para uso futuro.||  
|**adSchemaUsagePrivileges**|15|Retorna os privilégios de uso nos objetos definidos no catálogo que estão disponíveis para ou concedido por um determinado usuário.<br /><br /> (Conjunto de linhas USAGE_PRIVILEGES)|OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME OBJECT_TYPE CONCESSOR AO USUÁRIO AUTORIZADO|  
|**adSchemaViewColumnUsage**|24|Retorna as colunas nas quais exibidos tabelas, definidas no catálogo e pertencem a um determinado usuário, são dependentes.<br /><br /> (Conjunto de linhas VIEW_COLUMN_USAGE)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|Retorna as exibições definidas no catálogo que são acessíveis para um determinado usuário.<br /><br /> (Conjunto de linhas de modos de exibição)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaViewTableUsage**|25|Retorna as tabelas no qual exibidos tabelas, definidas no catálogo e pertencem a um determinado usuário, são dependentes.<br /><br /> (Conjunto de linhas VIEW_TABLE_USAGE)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
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
