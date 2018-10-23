---
title: Membros SQLServerDatabaseMetaData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 327ba0bc-438a-494c-b119-1cd4a096bb58
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95948680f7bd7bb1766207fa8894d274b5e09daf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788067"
---
# <a name="sqlserverdatabasemetadata-members"></a>Membros de SQLServerDatabaseMetaData
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pela classe [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md).  
  
## <a name="constructors"></a>Construtores  
 Nenhum.  
  
## <a name="fields"></a>Campos  
 Nenhum.  
  
## <a name="inherited-fields"></a>Campos herdados  
  
|Nome|Descrição|  
|----------|-----------------|  
|java.sql.DatabaseMetaData|attributeNoNulls, attributeNullable, attributeNullableUnknown, bestRowNotPseudo, bestRowPseudo, bestRowSession, bestRowTemporary, bestRowTransaction, bestRowUnknown, columnNoNulls, columnNullable, columnNullableUnknown, importedKeyCascade, importedKeyInitiallyDeferred, importedKeyInitiallyImmediate, importedKeyNoAction, importedKeyNotDeferrable, importedKeyRestrict, importedKeySetDefault, importedKeySetNull, procedureColumnIn, procedureColumnInOut, procedureColumnOut, procedureColumnResult, procedureColumnReturn, procedureColumnUnknown, procedureNoNulls, procedureNoResult, procedureNullable, procedureNullableUnknown, procedureResultUnknown, procedureReturnsResult, sqlStateSQL, sqlStateSQL99, sqlStateXOpen, tableIndexClustered, tableIndexHashed, tableIndexOther, tableIndexStatistic, typeNoNulls, typeNullable, typeNullableUnknown, typePredBasic, typePredChar, typePredNone, typeSearchable, versionColumnNotPseudo, versionColumnPseudo, versionColumnUnknown|  
  
## <a name="methods"></a>Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[allProceduresAreCallable](../../../connect/jdbc/reference/allproceduresarecallable-method-sqlserverdatabasemetadata.md)|Recupera se o usuário atual tem permissões para chamar todos os procedimentos retornados pelo método [getProcedures](../../../connect/jdbc/reference/getprocedures-method-sqlserverdatabasemetadata.md).|  
|[allTablesAreSelectable](../../../connect/jdbc/reference/alltablesareselectable-method-sqlserverdatabasemetadata.md)|Recupera se o usuário atual tem permissões para usar todas as tabelas retornadas pelo método [getTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md) em uma instrução SELECT.|  
|[autoCommitFailureClosesAllResultSets](../../../connect/jdbc/reference/autocommitfailureclosesallresultsets-method-sqlserverdatabasemetadata.md)|Indica se o driver JDBC fecha todos os conjuntos de resultados abertos, inclusive aqueles colocados em espera, quando uma confirmação automática é habilitada e uma exceção é lançada.|  
|[dataDefinitionCausesTransactionCommit](../../../connect/jdbc/reference/datadefinitioncausestransactioncommit-method-sqlserverdatabasemetadata.md)|Recupera se uma instrução de definição de dados de uma transação força a confirmação da transação.|  
|[dataDefinitionIgnoredInTransactions](../../../connect/jdbc/reference/datadefinitionignoredintransactions-method-sqlserverdatabasemetadata.md)|Recupera se o banco de dados em questão ignora uma instrução de definição de dados em uma transação.|  
|[deletesAreDetected](../../../connect/jdbc/reference/deletesaredetected-method-sqlserverdatabasemetadata.md)|Recupera se a exclusão de uma linha visível pode ser detectada ou não com a chamada do método [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) da classe [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).|  
|[doesMaxRowSizeIncludeBlobs](../../../connect/jdbc/reference/doesmaxrowsizeincludeblobs-method-sqlserverdatabasemetadata.md)|Recupera se o valor retornado do método [getMaxRowSize](../../../connect/jdbc/reference/getmaxrowsize-method-sqlserverdatabasemetadata.md) inclui os tipos de dados SQL LONGVARCHAR e LONGVARBINARY.|  
|[getAttributes](../../../connect/jdbc/reference/getattributes-method-sqlserverdatabasemetadata.md)|Recupera uma descrição do atributo especificado do tipo fornecido, para um tipo definido pelo usuário que está disponível no esquema e no catálogo fornecidos.|  
|[getBestRowIdentifier](../../../connect/jdbc/reference/getbestrowidentifier-method-sqlserverdatabasemetadata.md)|Recupera uma descrição do conjunto de colunas ideal de uma tabela que identifica exclusivamente uma linha.|  
|[getCatalogs](../../../connect/jdbc/reference/getcatalogs-method-sqlserverdatabasemetadata.md)|Recupera os nomes de catálogo disponíveis no servidor conectado.|  
|[getCatalogSeparator](../../../connect/jdbc/reference/getcatalogseparator-method-sqlserverdatabasemetadata.md)|Recupera a **String** usada por este banco de dados como o separador entre um catálogo e o nome da tabela.|  
|[getCatalogTerm](../../../connect/jdbc/reference/getcatalogterm-method-sqlserverdatabasemetadata.md)|Recupera o termo preferencial do fornecedor de banco de dados para "catalog".|  
|[getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md)|Recupera uma lista das propriedades de informações de cliente que têm o suporte do driver.|  
|[getColumnPrivileges](../../../connect/jdbc/reference/getcolumnprivileges-method-sqlserverdatabasemetadata.md)|Recupera uma descrição dos direitos de acesso das colunas de uma tabela.|  
|[getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md)|Recupera uma descrição das colunas da tabela que estão disponíveis no catálogo especificado.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatabasemetadata.md)|Recupera a conexão que produziu o objeto de metadados em questão.|  
|[getCrossReference](../../../connect/jdbc/reference/getcrossreference-method-sqlserverdatabasemetadata.md)|Recupera uma descrição das colunas de chave estrangeira da tabela de chaves estrangeiras fornecida que referencia as colunas de chave primária da tabela de chaves primárias fornecida.|  
|[getDatabaseMajorVersion](../../../connect/jdbc/reference/getdatabasemajorversion-method-sqlserverdatabasemetadata.md)|Recupera o número da versão principal do banco de dados subjacente.|  
|[getDatabaseMinorVersion](../../../connect/jdbc/reference/getdatabaseminorversion-method-sqlserverdatabasemetadata.md)|Recupera o número da versão secundária do banco de dados subjacente.|  
|[getDatabaseProductName](../../../connect/jdbc/reference/getdatabaseproductname-method-sqlserverdatabasemetadata.md)|Recupera o nome do produto desse banco de dados.|  
|[getDatabaseProductVersion](../../../connect/jdbc/reference/getdatabaseproductversion-method-sqlserverdatabasemetadata.md)|Recupera o número da versão do produto de banco de dados em questão.|  
|[getDefaultTransactionIsolation](../../../connect/jdbc/reference/getdefaulttransactionisolation-method-sqlserverdatabasemetadata.md)|Recupera o nível de isolamento de transação padrão do banco de dados em questão.|  
|[getDriverMajorVersion](../../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md)|Recupera o número de versão principal do driver JDBC em questão.|  
|[getDriverMinorVersion](../../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md)|Recupera o número de versão secundária desse JDBC Driver.|  
|[getDriverName](../../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md)|Recupera o nome do driver JDBC em questão.|  
|[getDriverVersion](../../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md)|Recupera o número de versão do driver JDBC em questão.|  
|[getExportedKeys](../../../connect/jdbc/reference/getexportedkeys-method-sqlserverdatabasemetadata.md)|Recupera uma descrição das colunas de chave estrangeira que referenciam as colunas de chave primária da tabela fornecida.|  
|[getExtraNameCharacters](../../../connect/jdbc/reference/getextranamecharacters-method-sqlserverdatabasemetadata.md)|Recupera todos os caracteres extras que podem ser usados em nomes de identificador sem aspas, por exemplo, aqueles além de a – z, A – Z, 0 – 9 e _.|  
|[getFunctions](../../../connect/jdbc/reference/getfunctions-method-sqlserverdatabasemetadata.md)|Recupera uma descrição das funções de sistema e de usuário.|  
|[getFunctionColumns](../../../connect/jdbc/reference/getfunctioncolumns-method-sqlserverdatabasemetadata.md)|Recupera uma descrição do sistema do catálogo especificado - ou parâmetros de função do usuário e tipo de retorno.|  
|[getIdentifierQuoteString](../../../connect/jdbc/reference/getidentifierquotestring-method-sqlserverdatabasemetadata.md)|Recupera a **String** usada para citar identificadores SQL.|  
|[getImportedKeys](../../../connect/jdbc/reference/getimportedkeys-method-sqlserverdatabasemetadata.md)|Recupera uma descrição das colunas de chave primária referenciadas pelas colunas de chave estrangeira de uma tabela.|  
|[getIndexInfo](../../../connect/jdbc/reference/getindexinfo-method-sqlserverdatabasemetadata.md)|Recupera uma descrição de índices e estatísticas da tabela fornecida.|  
|[getJDBCMajorVersion](../../../connect/jdbc/reference/getjdbcmajorversion-method-sqlserverdatabasemetadata.md)|Recupera o número da versão principal do JDBC desse driver.|  
|[getJDBCMinorVersion](../../../connect/jdbc/reference/getjdbcminorversion-method-sqlserverdatabasemetadata.md)|Recupera o número da versão secundária do JDBC para esse driver.|  
|[getMaxBinaryLiteralLength](../../../connect/jdbc/reference/getmaxbinaryliterallength-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de caracteres hexadecimais que o banco de dados em questão permite em uma literal binária embutida.|  
|[getMaxCatalogNameLength](../../../connect/jdbc/reference/getmaxcatalognamelength-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de caracteres que esse banco de dados permite em um nome de catálogo.|  
|[getMaxCharLiteralLength](../../../connect/jdbc/reference/getmaxcharliterallength-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de caracteres que o banco de dados em questão permite para uma literal de caractere.|  
|[getMaxColumnNameLength](../../../connect/jdbc/reference/getmaxcolumnnamelength-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de caracteres que o banco de dados em questão permite para um nome de coluna.|  
|[getMaxColumnsInGroupBy](../../../connect/jdbc/reference/getmaxcolumnsingroupby-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de colunas que o banco de dados permite em uma cláusula GROUP BY.|  
|[getMaxColumnsInIndex](../../../connect/jdbc/reference/getmaxcolumnsinindex-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de colunas que o banco de dados em questão permite em um índice.|  
|[getMaxColumnsInOrderBy](../../../connect/jdbc/reference/getmaxcolumnsinorderby-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de colunas que o banco de dados em questão permite em uma cláusula ORDER BY.|  
|[getMaxColumnsInSelect](../../../connect/jdbc/reference/getmaxcolumnsinselect-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de colunas que o banco de dados permite em uma lista SELECT.|  
|[getMaxColumnsInTable](../../../connect/jdbc/reference/getmaxcolumnsintable-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de colunas que o banco de dados em questão permite em uma tabela.|  
|[getMaxConnections](../../../connect/jdbc/reference/getmaxconnections-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de conexões simultâneas possíveis com esse banco de dados.|  
|[getMaxCursorNameLength](../../../connect/jdbc/reference/getmaxcursornamelength-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de caracteres que o banco de dados em questão permite em um nome de cursor.|  
|[getMaxIndexLength](../../../connect/jdbc/reference/getmaxindexlength-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de bytes que o banco de dados permite para um índice, incluindo todas as suas partes.|  
|[getMaxProcedureNameLength](../../../connect/jdbc/reference/getmaxprocedurenamelength-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de caracteres que esse banco de dados permite em um nome de procedimento.|  
|[getMaxRowSize](../../../connect/jdbc/reference/getmaxrowsize-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de bytes que esse banco de dados permite em uma única linha.|  
|[getMaxSchemaNameLength](../../../connect/jdbc/reference/getmaxschemanamelength-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de caracteres que esse banco de dados permite em um nome de esquema.|  
|[getMaxStatementLength](../../../connect/jdbc/reference/getmaxstatementlength-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de caracteres que o banco de dados em questão permite em uma instrução SQL.|  
|[getMaxStatements](../../../connect/jdbc/reference/getmaxstatements-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de instruções ativas para o banco de dados que podem ser abertas ao mesmo tempo.|  
|[getMaxTableNameLength](../../../connect/jdbc/reference/getmaxtablenamelength-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de caracteres que esse banco de dados permite em um nome de tabela.|  
|[getMaxTablesInSelect](../../../connect/jdbc/reference/getmaxtablesinselect-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de tabelas que o banco de dados em questão permite em uma instrução SELECT.|  
|[getMaxUserNameLength](../../../connect/jdbc/reference/getmaxusernamelength-method-sqlserverdatabasemetadata.md)|Recupera o número máximo de caracteres que o banco de dados em questão permite em um nome de usuário.|  
|[getNumericFunctions](../../../connect/jdbc/reference/getnumericfunctions-method-sqlserverdatabasemetadata.md)|Recupera uma lista separada por vírgulas de funções de matemática disponíveis com o banco de dados.|  
|[getPrimaryKeys](../../../connect/jdbc/reference/getprimarykeys-method-sqlserverdatabasemetadata.md)|Recupera uma descrição das colunas de chave primária da tabela fornecida.|  
|[getProcedureColumns](../../../connect/jdbc/reference/getprocedurecolumns-method-sqlserverdatabasemetadata.md)|Recupera uma descrição dos parâmetros de procedimento armazenado e das colunas de resultado.|  
|[getProcedures](../../../connect/jdbc/reference/getprocedures-method-sqlserverdatabasemetadata.md)|Recupera uma descrição dos procedimentos armazenados disponíveis no catálogo, esquema ou padrão de nome de procedimento armazenado fornecido.|  
|[getProcedureTerm](../../../connect/jdbc/reference/getprocedureterm-method-sqlserverdatabasemetadata.md)|Recupera o termo preferencial para "procedimento" no banco de dados em questão.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverdatabasemetadata.md)|Recupera a capacidade de colocação em espera padrão dos conjuntos de resultados do banco de dados em questão.|  
|[getRowIdLifetime](../../../connect/jdbc/reference/getrowidlifetime-method-sqlserverdatabasemetadata.md)|Retorna um status que indica se o tipo de dados SQL RowId tem suporte ou não. Se tiver, retorna o tempo de vida durante o qual um objeto RowId permanece válido.|  
|[getSchemas](../../../connect/jdbc/reference/getschemas-method.md)|Recupera os nomes de esquema disponíveis no banco de dados atual.|  
|[getSchemaTerm](../../../connect/jdbc/reference/getschematerm-method-sqlserverdatabasemetadata.md)|Recupera o termo preferencial para "esquema" no banco de dados em questão.|  
|[getSearchStringEscape](../../../connect/jdbc/reference/getsearchstringescape-method-sqlserverdatabasemetadata.md)|Recupera a **cadeia de caracteres** que pode ser usada para o escape de caracteres curinga.|  
|[getSQLKeywords](../../../connect/jdbc/reference/getsqlkeywords-method-sqlserverdatabasemetadata.md)|Recupera uma lista separada por vírgulas de todas as palavras-chave do SQL desse banco de dados que não são também palavras-chave do SQL92.|  
|[getSQLStateType](../../../connect/jdbc/reference/getsqlstatetype-method-sqlserverdatabasemetadata.md)|Indica se o SQLSTATE retornado pelo método SQLException.getSQLState é X/Open (agora conhecido como Open Group), SQL CLI, SQL99 (JDBC 3.0) ou SQL:2003 (JDBC 4.0).|  
|[getStringFunctions](../../../connect/jdbc/reference/getstringfunctions-method-sqlserverdatabasemetadata.md)|Recupera uma lista separada por vírgulas de funções **String** do sistema disponíveis com o banco de dados em questão.|  
|[getSuperTables](../../../connect/jdbc/reference/getsupertables-method-sqlserverdatabasemetadata.md)|Recupera uma descrição das hierarquias de tabela definidas em um esquema específico no banco de dados em questão.|  
|[getSuperTypes](../../../connect/jdbc/reference/getsupertypes-method-sqlserverdatabasemetadata.md)|Recupera uma descrição das hierarquias de tipos definidos pelo usuário em um esquema específico no banco de dados em questão.|  
|[getSystemFunctions](../../../connect/jdbc/reference/getsystemfunctions-method-sqlserverdatabasemetadata.md)|Recupera uma lista separada por vírgulas de funções do sistema disponíveis com o banco de dados em questão.|  
|[getTablePrivileges](../../../connect/jdbc/reference/gettableprivileges-method-sqlserverdatabasemetadata.md)|Recupera uma descrição dos direitos de acesso de cada tabela, disponível no padrão de nome de catálogo, esquema ou tabela fornecido.|  
|[getTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md)|Recupera uma descrição das tabelas disponíveis no padrão de nome de catálogo, esquema ou tabela fornecido.|  
|[getTableTypes](../../../connect/jdbc/reference/gettabletypes-method-sqlserverdatabasemetadata.md)|Recupera os tipos de tabela disponíveis no banco de dados atual.|  
|[getTimeDateFunctions](../../../connect/jdbc/reference/gettimedatefunctions-method-sqlserverdatabasemetadata.md)|Recupera uma lista separada por vírgulas de funções de hora e data disponíveis com esse banco de dados.|  
|[getTypeInfo](../../../connect/jdbc/reference/gettypeinfo-method-sqlserverdatabasemetadata.md)|Recupera uma descrição de todos os tipos SQL padrão que têm o suporte do banco de dados atual.|  
|[getUDTs](../../../connect/jdbc/reference/getudts-method-sqlserverdatabasemetadata.md)|Recupera uma descrição de tipos definidos pelo usuário em um esquema específico.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatabasemetadata.md)|Recupera a URL do banco de dados.|  
|[getUserName](../../../connect/jdbc/reference/getusername-method-sqlserverdatabasemetadata.md)|Recupera o nome de usuário como é conhecido para este banco de dados.|  
|[getVersionColumns](../../../connect/jdbc/reference/getversioncolumns-method-sqlserverdatabasemetadata.md)|Recupera uma descrição das colunas de uma tabela que é atualizada automaticamente quando qualquer valor em uma linha é atualizado.|  
|[insertsAreDetected](../../../connect/jdbc/reference/insertsaredetected-method-sqlserverdatabasemetadata.md)|Recupera se a inserção de uma linha visível pode ser detectada ou não com a chamada do método [rowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md) da classe [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).|  
|[isCatalogAtStart](../../../connect/jdbc/reference/iscatalogatstart-method-sqlserverdatabasemetadata.md)|Recupera se um catálogo aparece no início de um nome de tabela totalmente qualificado.|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados está no modo somente leitura.|  
|[locatorsUpdateCopy](../../../connect/jdbc/reference/locatorsupdatecopy-method-sqlserverdatabasemetadata.md)|Indica se as atualizações feitas em um LOB são feitas em uma cópia ou diretamente no LOB.|  
|[nullPlusNonNullIsNull](../../../connect/jdbc/reference/nullplusnonnullisnull-method-sqlserverdatabasemetadata.md)|Indica se esse banco de dados oferece suporte a concatenações entre valores NULL e não NULL que são NULL.|  
|[nullsAreSortedAtEnd](../../../connect/jdbc/reference/nullsaresortedatend-method-sqlserverdatabasemetadata.md)|Recupera se são classificados valores NULL no final independentemente da ordem de classificação.|  
|[nullsAreSortedAtStart](../../../connect/jdbc/reference/nullsaresortedatstart-method-sqlserverdatabasemetadata.md)|Recupera se são classificados valores NULL no início independentemente da ordem de classificação.|  
|[nullsAreSortedHigh](../../../connect/jdbc/reference/nullsaresortedhigh-method-sqlserverdatabasemetadata.md)|Recupera se os valores NULL são classificados de cima para baixo.|  
|[nullsAreSortedLow](../../../connect/jdbc/reference/nullsaresortedlow-method-sqlserverdatabasemetadata.md)|Recupera se os valores NULL são classificados de baixo para cima.|  
|[othersDeletesAreVisible](../../../connect/jdbc/reference/othersdeletesarevisible-method-sqlserverdatabasemetadata.md)|Recupera se as exclusões feitas por outros são visíveis.|  
|[othersInsertsAreVisible](../../../connect/jdbc/reference/othersinsertsarevisible-method-sqlserverdatabasemetadata.md)|Recupera se as inserções feitas por outros são visíveis.|  
|[othersUpdatesAreVisible](../../../connect/jdbc/reference/othersupdatesarevisible-method-sqlserverdatabasemetadata.md)|Recupera se as atualizações feitas por outros são visíveis.|  
|[ownDeletesAreVisible](../../../connect/jdbc/reference/owndeletesarevisible-method-sqlserverdatabasemetadata.md)|Recupera se as próprias exclusões de um conjunto de resultados são visíveis.|  
|[ownInsertsAreVisible](../../../connect/jdbc/reference/owninsertsarevisible-method-sqlserverdatabasemetadata.md)|Recupera se as próprias inserções de um conjunto de resultados são visíveis.|  
|[ownUpdatesAreVisible](../../../connect/jdbc/reference/ownupdatesarevisible-method-sqlserverdatabasemetadata.md)|Recupera se as próprias atualizações de um conjunto de resultados são visíveis.|  
|[storesLowerCaseIdentifiers](../../../connect/jdbc/reference/storeslowercaseidentifiers-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados trata identificadores de SQL que usam maiúsculas e minúsculas, e que não estão entre aspas, como sem diferenciação de maiúsculas e minúsculas e os armazena em minúsculas.|  
|[storesLowerCaseQuotedIdentifiers](../../../connect/jdbc/reference/storeslowercasequotedidentifiers-method-sqlserverdatabasemetadata.md)|Recupera se este banco de dados trata identificadores de SQL que usam maiúsculas e minúsculas, e que estão entre aspas, sem diferenciar maiúsculas e minúsculas e os armazena em minúsculas.|  
|[storesMixedCaseIdentifiers](../../../connect/jdbc/reference/storesmixedcaseidentifiers-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados trata identificadores SQL que usam maiúsculas e minúsculas, e que não estão entre aspas, como sem diferenciação de maiúsculas e minúsculas e os armazena em maiúsculas e minúsculas.|  
|[storesMixedCaseQuotedIdentifiers](../../../connect/jdbc/reference/storesmixedcasequotedidentifiers-method-sqlserverdatabasemetadata.md)|Recupera se este banco de dados trata identificadores de SQL que usam maiúsculas e minúsculas, e que estão entre aspas, com diferenciação de maiúsculas e minúsculas e os armazena em maiúsculas e minúsculas.|  
|[storesUpperCaseIdentifiers](../../../connect/jdbc/reference/storesuppercaseidentifiers-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados trata identificadores SQL que usam maiúsculas e minúsculas, e que não estão entre aspas, como sem diferenciação de maiúsculas e minúsculas e os armazena em maiúsculas.|  
|[storesUpperCaseQuotedIdentifiers](../../../connect/jdbc/reference/storesuppercasequotedidentifiers-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados trata identificadores de SQL que usam maiúsculas e minúsculas, e que estão entre aspas, como sem diferenciação de maiúsculas e minúsculas e os armazena em maiúsculas.|  
|[supportsAlterTableWithAddColumn](../../../connect/jdbc/reference/supportsaltertablewithaddcolumn-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a ALTER TABLE com add column.|  
|[supportsAlterTableWithDropColumn](../../../connect/jdbc/reference/supportsaltertablewithdropcolumn-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a ALTER TABLE com drop column.|  
|[supportsANSI92EntryLevelSQL](../../../connect/jdbc/reference/supportsansi92entrylevelsql-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte à gramática de SQL de nível entrada do padrão ANSI92.|  
|[supportsANSI92FullSQL](../../../connect/jdbc/reference/supportsansi92fullsql-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte à gramática de SQL completa do padrão ANSI92.|  
|[supportsANSI92IntermediateSQL](../../../connect/jdbc/reference/supportsansi92intermediatesql-method-sqlserverdatabasemetadata.md)|Recupera se este banco de dados oferece suporte à gramática de SQL intermediária do padrão ANSI92.|  
|[supportsBatchUpdates](../../../connect/jdbc/reference/supportsbatchupdates-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a atualizações em lote.|  
|[supportsCatalogsInDataManipulation](../../../connect/jdbc/reference/supportscatalogsindatamanipulation-method-sqlserverdatabasemetadata.md)|Recupera se um nome de catálogo pode ser usado em uma instrução de manipulação de dados.|  
|[supportsCatalogsInIndexDefinitions](../../../connect/jdbc/reference/supportscatalogsinindexdefinitions-method-sqlserverdatabasemetadata.md)|Recupera se um nome de catálogo pode ser usado em uma instrução de definição de índice.|  
|[supportsCatalogsInPrivilegeDefinitions](../../../connect/jdbc/reference/supportscatalogsinprivilegedefinitions-method-sqlserverdatabasemetadata.md)|Recupera se um nome de catálogo pode ser usado em uma instrução de definição de privilégios.|  
|[supportsCatalogsInProcedureCalls](../../../connect/jdbc/reference/supportscatalogsinprocedurecalls-method-sqlserverdatabasemetadata.md)|Recupera se um nome de catálogo pode ser usado em uma instrução de chamada de procedimento.|  
|[supportsCatalogsInTableDefinitions](../../../connect/jdbc/reference/supportscatalogsintabledefinitions-method-sqlserverdatabasemetadata.md)|Recupera se um nome de catálogo pode ser usado em uma instrução de definição de tabela.|  
|[supportsColumnAliasing](../../../connect/jdbc/reference/supportscolumnaliasing-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a aliases de colunas.|  
|[supportsConvert](../../../connect/jdbc/reference/supportsconvert-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte à função CONVERT entre tipos de SQL.|  
|[supportsCoreSQLGrammar](../../../connect/jdbc/reference/supportscoresqlgrammar-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte à gramática de SQL do núcleo do ODBC.|  
|[supportsCorrelatedSubqueries](../../../connect/jdbc/reference/supportscorrelatedsubqueries-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a subconsultas correlacionadas.|  
|[supportsDataDefinitionAndDataManipulationTransactions](../../../connect/jdbc/reference/supportsdatadefinitionanddatamanipulationtransactions-method.md)|Recupera se esse banco de dados oferece suporte a instruções de definição e manipulação de dados em uma transação.|  
|[supportsDataManipulationTransactionsOnly](../../../connect/jdbc/reference/supportsdatamanipulationtransactionsonly-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte somente a instruções de manipulação de dados em uma transação.|  
|[supportsDifferentTableCorrelationNames](../../../connect/jdbc/reference/supportsdifferenttablecorrelationnames-method-sqlserverdatabasemetadata.md)|Recupera se, quando há suporte a nomes de correlação de tabela, eles são restritos a nomes diferentes dos nomes de tabelas.|  
|[supportsExpressionsInOrderBy](../../../connect/jdbc/reference/supportsexpressionsinorderby-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a expressões em listas ORDER BY.|  
|[supportsExtendedSQLGrammar](../../../connect/jdbc/reference/supportsextendedsqlgrammar-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte à gramática de SQL estendida do ODBC.|  
|[supportsFullOuterJoins](../../../connect/jdbc/reference/supportsfullouterjoins-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a junções externas aninhadas completas.|  
|[supportsGetGeneratedKeys](../../../connect/jdbc/reference/supportsgetgeneratedkeys-method-sqlserverdatabasemetadata.md)|Recupera se as chaves geradas automaticamente podem ser recuperadas depois que uma instrução for executada.|  
|[supportsGroupBy](../../../connect/jdbc/reference/supportsgroupby-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a alguma forma da cláusula GROUP BY.|  
|[supportsGroupByBeyondSelect](../../../connect/jdbc/reference/supportsgroupbybeyondselect-method-sqlserverdatabasemetadata.md)|Recupera se este banco de dados dá suporte ao uso de colunas não incluídas na instrução SELECT em uma cláusula GROUP BY, contanto que todas as colunas da instrução SELECT sejam incluídas na cláusula GROUP BY.|  
|[supportsGroupByUnrelated](../../../connect/jdbc/reference/supportsgroupbyunrelated-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte ao uso de uma coluna que não está na instrução SELECT em uma cláusula GROUP BY.|  
|[supportsIntegrityEnhancementFacility](../../../connect/jdbc/reference/supportsintegrityenhancementfacility-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a SQL Integrity Enhancement Facility.|  
|[supportsLikeEscapeClause](../../../connect/jdbc/reference/supportslikeescapeclause-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte à especificação de uma cláusula de escape LIKE.|  
|[supportsLimitedOuterJoins](../../../connect/jdbc/reference/supportslimitedouterjoins-method-sqlserverdatabasemetadata.md)|Recupera se este banco de dados oferece suporte limitado a junções externas.|  
|[supportsMinimumSQLGrammar](../../../connect/jdbc/reference/supportsminimumsqlgrammar-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte à gramática de SQL mínima do ODBC.|  
|[supportsMixedCaseIdentifiers](../../../connect/jdbc/reference/supportsmixedcaseidentifiers-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados trata identificadores SQL que usam maiúsculas e minúsculas, e que não estão entre aspas, como sem diferenciação de maiúsculas e minúsculas e os armazena em maiúsculas e minúsculas.|  
|[supportsMixedCaseQuotedIdentifiers](../../../connect/jdbc/reference/supportsmixedcasequotedidentifiers-method-sqlserverdatabasemetadata.md)|Recupera se este banco de dados trata identificadores de SQL que usam maiúsculas e minúsculas, e que estão entre aspas, com diferenciação de maiúsculas e minúsculas e os armazena em maiúsculas e minúsculas.|  
|[supportsMultipleOpenResults](../../../connect/jdbc/reference/supportsmultipleopenresults-method-sqlserverdatabasemetadata.md)|Recupera se é possível ter vários objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) retornados simultaneamente de um objeto [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md).|  
|[supportsMultipleResultSets](../../../connect/jdbc/reference/supportsmultipleresultsets-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados é compatível com a obtenção de vários objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de uma única chamada ao método [execute](../../../connect/jdbc/reference/execute-method.md) da classe [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md).|  
|[supportsMultipleTransactions](../../../connect/jdbc/reference/supportsmultipletransactions-method-sqlserverdatabasemetadata.md)|Recupera se este banco de dados permite que várias transações sejam abertas ao mesmo tempo em conexões diferentes.|  
|[supportsNamedParameters](../../../connect/jdbc/reference/supportsnamedparameters-method-sqlserverdatabasemetadata.md)|Recupera se este banco de dados suporta parâmetros nomeados em instruções chamáveis.|  
|[supportsNonNullableColumns](../../../connect/jdbc/reference/supportsnonnullablecolumns-method-sqlserverdatabasemetadata.md)|Recupera se as colunas nesse banco de dados podem ser definidas como não anuláveis.|  
|[supportsOpenCursorsAcrossCommit](../../../connect/jdbc/reference/supportsopencursorsacrosscommit-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte à manutenção de cursores abertos entre confirmações.|  
|[supportsOpenCursorsAcrossRollback](../../../connect/jdbc/reference/supportsopencursorsacrossrollback-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte à manutenção de cursores abertos entre reversões.|  
|[supportsOpenStatementsAcrossCommit](../../../connect/jdbc/reference/supportsopenstatementsacrosscommit-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte à manutenção de instruções abertas entre confirmações.|  
|[supportsOpenStatementsAcrossRollback](../../../connect/jdbc/reference/supportsopenstatementsacrossrollback-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte à manutenção de instruções abertas entre reversões.|  
|[supportsOrderByUnrelated](../../../connect/jdbc/reference/supportsorderbyunrelated-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte ao uso de uma coluna que não está na instrução SELECT em uma cláusula ORDER BY.|  
|[supportsOuterJoins](../../../connect/jdbc/reference/supportsouterjoins-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a alguma forma de junção externa.|  
|[supportsPositionedDelete](../../../connect/jdbc/reference/supportspositioneddelete-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a instruções DELETE posicionadas.|  
|[supportsPositionedUpdate](../../../connect/jdbc/reference/supportspositionedupdate-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a instruções UPDATE posicionadas.|  
|[supportsResultSetConcurrency](../../../connect/jdbc/reference/supportsresultsetconcurrency-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte ao tipo de simultaneidade fornecido em combinação com o tipo do conjunto de resultados fornecido.|  
|[supportsResultSetHoldability](../../../connect/jdbc/reference/supportsresultsetholdability-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte à suspensão do conjunto de resultados fornecido.|  
|[supportsResultSetType](../../../connect/jdbc/reference/supportsresultsettype-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte ao tipo do conjunto de resultados fornecido.|  
|[supportsSavepoints](../../../connect/jdbc/reference/supportssavepoints-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a pontos de salvamento.|  
|[supportsSchemasInDataManipulation](../../../connect/jdbc/reference/supportsschemasindatamanipulation-method-sqlserverdatabasemetadata.md)|Recupera se um nome de esquema pode ser usado em uma instrução de manipulação de dados.|  
|[supportsSchemasInIndexDefinitions](../../../connect/jdbc/reference/supportsschemasinindexdefinitions-method-sqlserverdatabasemetadata.md)|Recupera se um nome de esquema pode ser usado em uma instrução de definição de índice.|  
|[supportsSchemasInPrivilegeDefinitions](../../../connect/jdbc/reference/supportsschemasinprivilegedefinitions-method-sqlserverdatabasemetadata.md)|Recupera se um nome de esquema pode ser usado em uma instrução de definição de privilégios.|  
|[supportsSchemasInProcedureCalls](../../../connect/jdbc/reference/supportsschemasinprocedurecalls-method-sqlserverdatabasemetadata.md)|Recupera se um nome de esquema pode ser usado em uma instrução de chamada de procedimento.|  
|[supportsSchemasInTableDefinitions](../../../connect/jdbc/reference/supportsschemasintabledefinitions-method-sqlserverdatabasemetadata.md)|Recupera se um nome de esquema pode ser usado em uma instrução de definição de tabela.|  
|[supportsSelectForUpdate](../../../connect/jdbc/reference/supportsselectforupdate-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a instruções SELECT FOR UPDATE.|  
|[supportsStatementPooling](../../../connect/jdbc/reference/supportsstatementpooling-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte ao pooling de instrução.|  
|[supportsStoredFunctionsUsingCallSyntax](../../../connect/jdbc/reference/supportsstoredfunctionsusingcallsyntax-method-sqlserverdatabasemetadata.md)|Indica se o banco de dados atual dá suporte à invocação de funções definidas pelo usuário ou pelo fornecedor usando a sintaxe de escape de procedimento armazenado.|  
|[supportsStoredProcedures](../../../connect/jdbc/reference/supportsstoredprocedures-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a chamadas de procedimento armazenado que usam a sintaxe de escape de procedimento armazenado.|  
|[supportsSubqueriesInComparisons](../../../connect/jdbc/reference/supportssubqueriesincomparisons-method-sqlserverdatabasemetadata.md)|Recupera se este banco de dados dá suporte a subconsultas em expressões de comparação.|  
|[supportsSubqueriesInExists](../../../connect/jdbc/reference/supportssubqueriesinexists-method-sqlserverdatabasemetadata.md)|Recupera se este banco de dados dá suporte a subconsultas em expressões EXISTS.|  
|[supportsSubqueriesInIns](../../../connect/jdbc/reference/supportssubqueriesinins-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a subconsultas em instruções IN.|  
|[supportsSubqueriesInQuantifieds](../../../connect/jdbc/reference/supportssubqueriesinquantifieds-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a subconsultas em expressões quantificadas.|  
|[supportsTableCorrelationNames](../../../connect/jdbc/reference/supportstablecorrelationnames-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a nomes de correlação de tabela.|  
|[supportsTransactionIsolationLevel](../../../connect/jdbc/reference/supportstransactionisolationlevel-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte ao nível de isolamento de transação fornecido.|  
|[supportsTransactions](../../../connect/jdbc/reference/supportstransactions-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a transações.|  
|[supportsUnion](../../../connect/jdbc/reference/supportsunion-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a SQL UNION.|  
|[supportsUnionAll](../../../connect/jdbc/reference/supportsunionall-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados oferece suporte a SQL UNION ALL.|  
|[updatesAreDetected](../../../connect/jdbc/reference/updatesaredetected-method-sqlserverdatabasemetadata.md)|Recupera se a atualização de uma linha visível pode ser detectada ou não com a chamada do método [rowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md) da classe [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).|  
|[usesLocalFilePerTable](../../../connect/jdbc/reference/useslocalfilepertable-method-sqlserverdatabasemetadata.md)|Recupera se este banco de dados usa um arquivo para cada tabela.|  
|[usesLocalFiles](../../../connect/jdbc/reference/useslocalfiles-method-sqlserverdatabasemetadata.md)|Recupera se esse banco de dados armazena tabelas em um arquivo local.|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Consulte Também  
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
