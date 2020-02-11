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
ms.openlocfilehash: c064120e3c658cafd88a96953ff00e18fbaa9b88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931119"
---
# <a name="schemaenum"></a>SchemaEnum
Especifica o tipo de **conjunto de registros** de esquema que o método [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) recupera.  
  
## <a name="remarks"></a>Comentários  
 Informações adicionais sobre a função e as colunas retornadas para cada constante ADO podem ser encontradas em tópicos no [Apêndice B: conjuntos](https://msdn.microsoft.com/2b5fbf03-e50d-44ee-bc57-5a57666c55f1) de linhas de esquema da referência do programador de OLE DB. O nome de cada tópico é listado entre parênteses na seção Descrição da tabela a seguir.  
  
 Informações adicionais sobre a função e as colunas retornadas para cada constante ADO MD podem ser encontradas em tópicos em [OLE DB para objetos OLAP e conjuntos](https://msdn.microsoft.com/d20bb2a6-68bd-423f-9ec8-eb930cd0c144) de linhas de esquema no OLE DB para documentação do processamento analítico online (OLAP). O nome de cada tópico é listado entre parênteses na coluna Descrição da tabela a seguir.  
  
 Você pode converter os tipos de dados de colunas na documentação do OLE DB em tipos de dados do ADO referindo-se à coluna Descrição do tópico ADO [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) . Por exemplo, um tipo de dados OLE DB de **DBTYPE_WSTR** é equivalente a um tipo de dados ADO de **adWChar**.  
  
 O ADO gera resultados semelhantes a esquema para as constantes, **adSchemaDBInfoKeywords** e **adSchemaDBInfoLiterals**. O ADO cria um **conjunto de registros**e, em seguida, preenche cada linha com os valores retornados respectivamente pelos métodos **IDBInfo:: GetKeywords** e **IDBInfo:: GetLiteralInfo** . Informações adicionais sobre esses métodos podem ser encontradas na seção [IDBInfo](https://msdn.microsoft.com/3f5ad97f-3fc6-4f21-b691-f6911e4007f3) da referência do programador de OLE DB.  
  
|Constante|Valor|DESCRIÇÃO|Colunas de restrição|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|Retorna as asserções definidas no catálogo que pertencem a um determinado usuário.<br /><br /> (Conjunto de linhas de ASSERções)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|Retorna os atributos físicos associados aos catálogos acessíveis a partir do DBMS.<br /><br /> (Conjunto de linhas de CATÁLOGOs)|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|Retorna os conjuntos de caracteres definidos no catálogo que são acessíveis a um determinado usuário.<br /><br /> (CHARACTER_SETS conjunto de linhas)|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|Retorna as restrições de verificação definidas no catálogo que pertencem a um determinado usuário.<br /><br /> (CHECK_CONSTRAINTS) Linhas|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|Retorna os agrupamentos de caracteres definidos no catálogo que são acessíveis a um determinado usuário.<br /><br /> (Conjunto de linhas de AGRUPAMENTOs)|COLLATION_CATALOG COLLATION_SCHEMA COLLATION_NAME|  
|**adSchemaColumnPrivileges**|13|Retorna os privilégios em colunas de tabelas definidas no catálogo que estão disponíveis para o, ou concedidas pelo, um determinado usuário.<br /><br /> (COLUMN_PRIVILEGES conjunto de linhas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|**adSchemaColumns**|4|Retorna as colunas de tabelas (incluindo exibições) definidas no catálogo que são acessíveis a um determinado usuário.<br /><br /> (Conjunto de linhas de colunas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|Retorna as colunas definidas no catálogo que dependem de um domínio definido no catálogo e de propriedade de um determinado usuário.<br /><br /> (COLUMN_DOMAIN_USAGE conjunto de linhas)|DOMAIN_CATALOG DOMAIN_SCHEMA DOMAIN_NAME COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|Retorna as colunas usadas por restrições referenciais, restrições exclusivas, restrições de verificação e asserções, definidas no catálogo e de propriedade de um determinado usuário.<br /><br /> (CONSTRAINT_COLUMN_USAGE conjunto de linhas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|Retorna as tabelas usadas por restrições referenciais, restrições exclusivas, restrições de verificação e asserções definidas no catálogo e de propriedade de um determinado usuário.<br /><br /> (CONSTRAINT_TABLE_USAGE conjunto de linhas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaCubes**|32|Retorna informações sobre os cubos disponíveis em um esquema (ou o catálogo, se o provedor não oferecer suporte a esquemas).<br /><br /> (Conjunto de linhas de CUBOs *)|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|Retorna uma lista de palavras-chave específicas do provedor.<br /><br /> (IDBInfo:: getpalavra-chave)|\<Nenhum>|  
|**adSchemaDBInfoLiterals**|31|Retorna uma lista de literais específicos do provedor usados em comandos de texto.<br /><br /> (IDBInfo:: GetLiteralInfo)|\<Nenhum>|  
|**adSchemaDimensions**|33|Retorna informações sobre as dimensões em um determinado cubo. Ele tem uma linha para cada dimensão.<br /><br /> (Conjunto de linhas DIMENSIONs)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|Retorna as colunas de chave estrangeira definidas no catálogo por um determinado usuário.<br /><br /> (FOREIGN_KEYS conjunto de linhas)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|Retorna informações sobre as hierarquias disponíveis em uma dimensão.<br /><br /> (Conjunto de linhas de HIERARQUIAs)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|Retorna os índices definidos no catálogo que pertencem a um determinado usuário.<br /><br /> (Conjunto de linhas de índices)|TIPO DE INDEX_NAME DE TABLE_SCHEMA DE TABLE_CATALOG TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|Retorna as colunas definidas no catálogo que são restritas como chaves por um determinado usuário.<br /><br /> (KEY_COLUMN_USAGE conjunto de linhas)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaLevels**|35|Retorna informações sobre os níveis disponíveis em uma dimensão.<br /><br /> (Conjunto de linhas de níveis)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_NAME LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|Retorna informações sobre as medidas disponíveis.<br /><br /> (Conjunto de linhas MEASUREs)|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|Retorna informações sobre os membros disponíveis.<br /><br /> (Conjunto de linhas Membros)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE Tree Operator. Para obter mais informações, consulte OLE DB para OLAP (processamento analítico online).|  
|**adSchemaPrimaryKeys**|28|Retorna as colunas de chave primária definidas no catálogo por um determinado usuário.<br /><br /> (PRIMARY_KEYS conjunto de linhas)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|Retorna informações sobre as colunas de conjuntos de linhas retornadas por procedimentos.<br /><br /> (PROCEDURE_COLUMNS conjunto de linhas)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|Retorna informações sobre os parâmetros e códigos de retorno de procedimentos.<br /><br /> (PROCEDURE_PARAMETERS conjunto de linhas)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|**adSchemaProcedures**|16|Retorna os procedimentos definidos no catálogo que pertencem a um determinado usuário.<br /><br /> (Conjunto de linhas de procedimentos)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|Retorna informações sobre as propriedades disponíveis para cada nível da dimensão.<br /><br /> (Conjunto de linhas Propriedades)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|Usado se o provedor definir suas próprias consultas de esquema não padrão.|\<> específicas do provedor|  
|**adSchemaProviderTypes**|22|Retorna os tipos de dados (base) suportados pelo provedor de dados.<br /><br /> (PROVIDER_TYPES conjunto de linhas)|DATA_TYPE BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|Retorna as restrições referenciais definidas no catálogo que pertencem a um determinado usuário.<br /><br /> (REFERENTIAL_CONSTRAINTS conjunto de linhas)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|Retorna os esquemas (objetos de banco de dados) que pertencem a um determinado usuário.<br /><br /> (Conjunto de linhas SCHEMATA)|CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|Retorna os níveis de conformidade, as opções e os dialetos suportados pelos dados de processamento da implementação SQL definidos no catálogo.<br /><br /> (SQL_LANGUAGES conjunto de linhas)|\<Nenhum>|  
|**adSchemaStatistics**|19|Retorna as estatísticas definidas no catálogo que pertencem a um determinado usuário.<br /><br /> (Conjunto de linhas de estatísticas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaTableConstraints**|10|Retorna as restrições de tabela definidas no catálogo que pertencem a um determinado usuário.<br /><br /> (TABLE_CONSTRAINTS conjunto de linhas)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|Retorna os privilégios em tabelas definidas no catálogo que estão disponíveis para o, ou concedidas pelo, um determinado usuário.<br /><br /> (TABLE_PRIVILEGES conjunto de linhas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|**adSchemaTables**|20|Retorna as tabelas (incluindo exibições) definidas no catálogo que são acessíveis a um determinado usuário.<br /><br /> (Conjunto de linhas de tabelas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|**adSchemaTranslations**|21|Retorna as conversões de caracteres definidas no catálogo que são acessíveis a um determinado usuário.<br /><br /> (Conjunto de linhas de TRADUções)|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|11,8|Reservado para uso futuro.||  
|**adSchemaUsagePrivileges**|15|Retorna os privilégios de uso em objetos definidos no catálogo que estão disponíveis para o, ou concedidos pelo, um determinado usuário.<br /><br /> (USAGE_PRIVILEGES conjunto de linhas)|OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME OBJECT_TYPE CONCESSOR ENTIDADE AUTORIZADA|  
|**adSchemaViewColumnUsage**|24|Retorna as colunas nas quais as tabelas exibidas, definidas no catálogo e de propriedade de um determinado usuário, são dependentes.<br /><br /> (VIEW_COLUMN_USAGE conjunto de linhas)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|Retorna as exibições definidas no catálogo que são acessíveis a um determinado usuário.<br /><br /> (Conjunto de linhas views)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaViewTableUsage**|25|Retorna as tabelas nas quais as tabelas exibidas, definidas no catálogo e de propriedade de um determinado usuário, são dependentes.<br /><br /> (VIEW_TABLE_USAGE conjunto de linhas)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. Schema. ASSERTs|  
|AdoEnums. Schema. CATALOGs|  
|AdoEnums. Schema. CHARACTERSETS|  
|AdoEnums. Schema. CHECKCONSTRAINTS|  
|AdoEnums. Schema. AGRUPAMENTOs|  
|AdoEnums. Schema. COLUMNPRIVILEGES|  
|AdoEnums. Schema. COLUMNS|  
|AdoEnums. Schema. COLUMNSDOMAINUSAGE|  
|AdoEnums. Schema. CONSTRAINTCOLUMNUSAGE|  
|AdoEnums. Schema. CONSTRAINTTABLEUSAGE|  
|AdoEnums. Schema. CUBEs|  
|AdoEnums. Schema. DBINFOKEYWORDS|  
|AdoEnums. Schema. DBINFOLITERALS|  
|AdoEnums. Schema. DIMENSIONs|  
|AdoEnums. Schema. FOREIGNKEYS|  
|AdoEnums. Schema. HIERARQUIAs|  
|AdoEnums. Schema. Indexes|  
|AdoEnums. Schema. KEYCOLUMNUSAGE|  
|AdoEnums. Schema. LEVELs|  
|AdoEnums. Schema. MEASUREs|  
|AdoEnums. Schema. MEMBERs|  
|AdoEnums. Schema. PRIMARYKEY|  
|AdoEnums. Schema. PROCEDURECOLUMNS|  
|AdoEnums. Schema. PROCEDUREparameters|  
|AdoEnums. Schema. PROCEDUREs|  
|AdoEnums. Schema. PROPERTIES|  
|AdoEnums. Schema. PROVIDERSPECIFIC|  
|AdoEnums. Schema. PROVIDERTYPES|  
|AdoEnums. Schema. REFERENTIALCONTRAINTS|  
|AdoEnums. Schema. SCHEMATA|  
|AdoEnums. Schema. sqlidiomas|  
|AdoEnums. Schema. STATISTICs|  
|AdoEnums. Schema. TABLECONSTRAINTS|  
|AdoEnums. Schema. TABLEPRIVILEGES|  
|AdoEnums. Schema. TABLEs|  
|AdoEnums. Schema. TRANSLATIONs|  
|AdoEnums. Schema. TRUSTers|  
|AdoEnums. Schema. USAGEPRIVILEGES|  
|AdoEnums. Schema. VIEWCOLUMNUSAGE|  
|AdoEnums. Schema. views|  
|AdoEnums. Schema. VIEWTABLEUSAGE|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
