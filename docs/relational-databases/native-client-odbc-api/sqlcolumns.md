---
title: SQLColumns | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLColumns function
ms.assetid: 69d3af44-8196-43ab-8037-cdd06207b171
caps.latest.revision: "62"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32a52df92152204237756ffcc07bafdbcd69c260
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sqlcolumns"></a>SQLColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLColumns** retorna SQL_SUCCESS se existirem ou não valores para o *CatalogName*, *TableName*, ou *ColumnName* parâmetros. **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
> [!NOTE]  
>  Para tipos de valores grandes, os parâmetros de todos os comprimentos serão retornados com um valor SQL_SS_LENGTH_UNLIMITED.  
  
 **SQLColumns** pode ser executado em um cursor de servidor estático. Uma tentativa de executar **SQLColumns** em um cursor atualizável (dinâmico ou conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO, indicando que o tipo de cursor foi alterado.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a informações de relatórios para tabelas em servidores vinculados, aceitando um nome de duas partes para o *CatalogName* parâmetro: *linked_server_name*.  
  
 Para ODBC 2. *x* aplicativos não usam curingas em *TableName*, **SQLColumns** retorna informações sobre quaisquer tabelas cujo nomes correspondem ao *TableName*e pertencem ao usuário atual. Se o usuário atual não possuir nenhuma tabela cujo nome corresponda a *TableName* parâmetro **SQLColumns** retorna informações sobre quaisquer tabelas pertencentes a outros usuários em que o nome da tabela corresponde a  *TableName* parâmetro. Para ODBC 2. *x* aplicativos usando caracteres curinga, **SQLColumns** retorna todas as tabelas cujo nomes correspondem ao *TableName*. Para ODBC 3. *x* aplicativos **SQLColumns** retorna todas as tabelas cujo nomes correspondem ao *TableName* independentemente do proprietário ou se os caracteres curinga é usada.  
  
 A tabela a seguir lista as colunas retornadas pelo conjunto de resultados:  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|DATA_TYPE|Retorna SQL_VARCHAR, SQL_VARBINARY ou SQL_WVARCHAR para o **varchar (max)** tipos de dados.|  
|TYPE_NAME|Retorna "varchar", "varbinary" ou "nvarchar" para o **varchar (max)**, **varbinary (max)**, e **nvarchar (max)** tipos de dados.|  
|COLUMN_SIZE|Retorna SQL_SS_LENGTH_UNLIMITED para **varchar (max)** indicando de tipos de dados que o tamanho da coluna é ilimitado.|  
|BUFFER_LENGTH|Retorna SQL_SS_LENGTH_UNLIMITED para **varchar (max)** indicando de tipos de dados que o tamanho do buffer é ilimitado.|  
|SQL_DATA_TYPE|Retorna SQL_VARCHAR, SQL_VARBINARY ou SQL_WVARCHAR para o **varchar (max)** tipos de dados.|  
|CHAR_OCTET_LENGTH|Retorna o comprimento máximo de uma coluna char ou binary. Retorna 0 para indicar que o tamanho é ilimitado.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|Retorna o nome do catálogo no qual é definido o nome de uma coleção de esquemas XML. Se não for possível localizar o nome do catálogo, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|Retorna o nome do esquema no qual é definido o nome de uma coleção de esquemas XML. Se não for possível localizar o nome do esquema, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_XML_SCHEMACOLLECTION_NAME|Retorna o nome de uma coleção de esquemas XML. Se não for possível localizar o nome, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_UDT_CATALOG_NAME|O nome do catálogo que contém o UDT (tipo definido pelo usuário).|  
|SS_UDT_SCHEMA_NAME|O nome do esquema que contém o UDT.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|O nome qualificado do assembly do UDT.|  
  
 Para UDTs, a coluna TYPE_NAME existente é usada para indicar o nome do UDT; Portanto, nenhuma coluna adicional deve ser adicionada ao conjunto de resultados de **SQLColumns** ou [SQLProcedureColumns](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md). O DATA_TYPE de uma coluna ou parâmetro UDT é SQL_SS_UDT.  
  
 Para o UDT de parâmetros, você pode usar os novos descritores específicos do driver definidos acima para obter ou definir as propriedades extra de metadados de um UDT, caso o servidor retorne ou exija essas informações.  
  
 Quando um cliente se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e chama SQLColumns, usando valores curinga ou NULL para o parâmetro de entrada de catálogo não retornará informações de outros catálogos. Em vez disso, serão retornadas apenas informações sobre o catálogo atual. O cliente pode chamar primeiro SQLTables para determinar em qual catálogo está localizada a tabela desejada. O cliente, em seguida, pode usar o valor do catálogo para o parâmetro de entrada de catálogo na chamada de SQLColumns para recuperar informações sobre as colunas na tabela.  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>SQLColumns e parâmetros com valor de tabela  
 O conjunto de resultados retornados por SQLColumns depende da configuração de SQL_SOPT_SS_NAME_SCOPE. Para obter mais informações, consulte [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). As colunas a seguir foram adicionadas para parâmetros com valor de tabela:  
  
|Nome da coluna|Tipo de dados|Sumário|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|Para uma coluna em um TABLE_TYPE, será SQL_TRUE se a coluna for uma coluna computada; caso contrário, SQL_FALSE.|  
|SS_IS_IDENTITY|Smallint|SQL_TRUE se a coluna for uma coluna de identidade; caso contrário, SQL_FALSE.|  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>Suporte de SQLColumns a recursos aprimorados de data e hora  
 Para obter informações sobre os valores retornados para tipos de data/hora, consulte [metadados de catálogo](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obter mais informações, consulte [data e hora melhorias &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>Suporte de SQLColumns para UDTs CLR grandes  
 **SQLColumns** oferece suporte a grandes CLR definido pelo usuário (UDTs tipos). Para obter mais informações, consulte [Large CLR User-Defined tipos &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>Suporte de SQLColumns para colunas esparsas  
 Dois [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] colunas específicas foram adicionadas ao conjunto de resultados de SQLColumns:  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|**Smallint**|Se a coluna for uma coluna esparsa, será SQL_TRUE; caso contrário, SQL_FALSE.|  
|SS_IS_COLUMN_SET|**Smallint**|Se a coluna for a **column_set** coluna, será SQL_TRUE; caso contrário, SQL_FALSE.|  
  
 Em conformidade com a especificação de ODBC, SS_IS_SPARSE e SS_IS_COLUMN_SET aparecem antes de todas as colunas específicas de driver que foram adicionadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versões anteriores [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]e depois de todas as colunas autorizadas pelo próprio ODBC.  
  
 O conjunto de resultados retornados por SQLColumns depende da configuração de SQL_SOPT_SS_NAME_SCOPE. Para obter mais informações, consulte [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Para obter mais informações sobre colunas esparsas no ODBC, consulte [suporte a colunas esparsas &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLColumns](http://go.microsoft.com/fwlink/?LinkId=59336)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
