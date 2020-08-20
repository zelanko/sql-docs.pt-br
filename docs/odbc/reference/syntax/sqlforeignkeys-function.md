---
description: Função SQLForeignKeys
title: Função SQLForeignKeys | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLForeignKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLForeignKeys
helpviewer_keywords:
- SQLForeignKeys function [ODBC]
ms.assetid: 07f3f645-f643-4d39-9a10-70a72f24e608
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 802153837d53c6886b44511fbdffe6efa6b83281
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491299"
---
# <a name="sqlforeignkeys-function"></a>Função SQLForeignKeys
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ODBC  
  
 **Resumo**  
 **SQLForeignKeys** pode retornar:  
  
-   Uma lista de chaves estrangeiras na tabela especificada (colunas na tabela especificada que se referem a chaves primárias em outras tabelas).  
  
-   Uma lista de chaves estrangeiras em outras tabelas que se referem à chave primária na tabela especificada.  
  
 O driver retorna cada lista como um conjunto de resultados na instrução especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLForeignKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      PKCatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      PKSchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      PKTableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      FKCatalogName,  
     SQLSMALLINT    NameLength4,  
     SQLCHAR *      FKSchemaName,  
     SQLSMALLINT    NameLength5,  
     SQLCHAR *      FKTableName,  
     SQLSMALLINT    NameLength6);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *PKCatalogName*  
 Entrada Nome do catálogo da tabela de chave primária. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") denota as tabelas que não têm catálogos. *PKCatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *PKCatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *PKCatalogName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 Entrada Comprimento de **PKCatalogName*, em caracteres.  
  
 *PKSchemaName*  
 Entrada Nome do esquema da tabela de chave primária. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") denota as tabelas que não têm esquemas. *PKSchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *PKSchemaName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *PKSchemaName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength2*  
 Entrada Comprimento de **PKSchemaName*, em caracteres.  
  
 *PKTableName*  
 Entrada Nome da tabela de chave primária. *PKTableName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *PKTableName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *PKTableName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength3*  
 Entrada Comprimento de **PKTableName*, em caracteres.  
  
 *FKCatalogName*  
 Entrada Nome do catálogo da tabela de chave estrangeira. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") denota as tabelas que não têm catálogos. *FKCatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *FKCatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *FKCatalogName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength4*  
 Entrada Comprimento de **FKCatalogName*, em caracteres.  
  
 *FKSchemaName*  
 Entrada Nome do esquema da tabela de chave estrangeira. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") denota as tabelas que não têm esquemas. *FKSchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *FKSchemaName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *FKSchemaName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength5*  
 Entrada Comprimento de **FKSchemaName*, em caracteres.  
  
 *FKTableName*  
 Entrada Nome da tabela de chave estrangeira. *FKTableName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *FKTableName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *FKTableName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength6*  
 Entrada Comprimento de **FKTableName*, em caracteres.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLForeignKeys** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLForeignKeys** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|24.000|Estado de cursor inválido|Um cursor estava aberto no *StatementHandle*e **SQLFetch** ou **SQLFetchScroll** foi chamado. Esse erro será retornado pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e será retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tiver retornado SQL_NO_DATA.<br /><br /> Um cursor estava aberto no *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tinha sido chamado.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado em *StatementHandle*e, em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|(DM) os argumentos *PKTableName* e *FKTableName* eram ambos ponteiros nulos.<br /><br /> O atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o argumento *FKCatalogName* ou *PKCatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes de catálogo têm suporte.<br /><br /> (DM) o atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *FKSchemaName*, *PKSchemaName*, *FKTableName*ou *PKTableName* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função SQLForeignKeys foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor de um dos argumentos de comprimento do nome era menor que 0, mas não é igual a SQL_NTS.|  
|||O valor de um dos argumentos de comprimento do nome excedeu o valor de comprimento máximo para o nome correspondente. (Consulte "Comentários".)|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um nome de catálogo foi especificado e o driver ou a fonte de dados não oferece suporte a catálogos.<br /><br /> Um nome de esquema foi especificado e o driver ou a fonte de dados não oferece suporte a esquemas.|  
|||A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era suportada pelo driver ou pela fonte de dados.<br /><br /> O atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não dá suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações sobre como as informações retornadas por essa função podem ser usadas, consulte [usos de dados do catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Se \* *PKTableName* contiver um nome de tabela, **SQLForeignKeys** retornará um conjunto de resultados que contém a chave primária da tabela especificada e todas as chaves estrangeiras que fazem referência a ela. A lista de chaves estrangeiras em outras tabelas não inclui chaves estrangeiras que apontam para restrições exclusivas na tabela especificada.  
  
 Se \* *FKTableName* contiver um nome de tabela, **SQLForeignKeys** retornará um conjunto de resultados que contém todas as chaves estrangeiras na tabela especificada que apontam para chaves primárias em outras tabelas e as chaves primárias nas outras tabelas às quais elas se referem. A lista de chaves estrangeiras na tabela especificada não contém chaves estrangeiras que se referem a restrições exclusivas em outras tabelas.  
  
 Se \* *PKTableName* e \* *FKTableName* contiverem nomes de tabela, **SQLForeignKeys** retornará as chaves estrangeiras na tabela especificada em \* *FKTableName* que se referem à chave primária da tabela especificada em **PKTableName*. Deve ser uma chave no máximo.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados de funções de catálogo ODBC, consulte [Catalog Functions](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLForeignKeys** retorna resultados como um conjunto de resultados padrão. Se as chaves estrangeiras associadas a uma chave primária forem solicitadas, o conjunto de resultados será ordenado por FKTABLE_CAT, FKTABLE_SCHEM, FKTABLE_NAME e KEY_SEQ. Se as chaves primárias associadas a uma chave estrangeira forem solicitadas, o conjunto de resultados será ordenado por PKTABLE_CAT, PKTABLE_SCHEM, PKTABLE_NAME e KEY_SEQ. A tabela a seguir lista as colunas no conjunto de resultados.  
  
 Os comprimentos das colunas VARCHAR não são mostrados na tabela; os comprimentos reais dependem da fonte de dados. Para determinar os comprimentos reais das PKTABLE_CAT ou FKTABLE_CAT, PKTABLE_SCHEM ou FKTABLE_SCHEM, PKTABLE_NAME ou FKTABLE_NAME, e PKCOLUMN_NAME ou FKCOLUMN_NAME colunas, um aplicativo pode chamar **SQLGetInfo** com as opções SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
 As colunas a seguir foram renomeadas para ODBC 3 *. x.* As alterações de nome de coluna não afetam a compatibilidade com versões anteriores porque os aplicativos são associados por número de coluna.  
  
|Coluna ODBC 2,0|Coluna ODBC 3 *. x*|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 14 (comentários) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas de driver, contando a partir do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados por funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1,0)|1|Varchar|Nome do catálogo da tabela de chave primária; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm catálogos.|  
|PKTABLE_SCHEM (ODBC 1,0)|2|Varchar|Nome do esquema da tabela de chave primária; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm esquemas.|  
|PKTABLE_NAME (ODBC 1,0)|3|Varchar não nulo|Nome da tabela de chave primária.|  
|PKCOLUMN_NAME (ODBC 1,0)|4|Varchar não nulo|Nome da coluna de chave primária. O driver retorna uma cadeia de caracteres vazia para uma coluna que não tem um nome.|  
|FKTABLE_CAT (ODBC 1,0)|5|Varchar|Nome do catálogo da tabela de chave estrangeira; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm catálogos.|  
|FKTABLE_SCHEM (ODBC 1,0)|6|Varchar|Nome do esquema da tabela de chave estrangeira; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm esquemas.|  
|FKTABLE_NAME (ODBC 1,0)|7|Varchar não nulo|Nome da tabela de chave estrangeira.|  
|FKCOLUMN_NAME (ODBC 1,0)|8|Varchar não nulo|Nome da coluna de chave estrangeira. O driver retorna uma cadeia de caracteres vazia para uma coluna que não tem um nome.|  
|KEY_SEQ (ODBC 1,0)|9|Smallint não NULL|Número de sequência da coluna na chave (começando com 1).|  
|UPDATE_RULE (ODBC 1,0)|10|Smallint|Ação a ser aplicada à chave estrangeira quando a operação SQL for **atualizada**. Pode ter um dos valores a seguir. (A tabela referenciada é a tabela que tem a chave primária; a tabela de referência é a tabela que tem a chave estrangeira.)<br /><br /> SQL_CASCADE: quando a chave primária da tabela referenciada é atualizada, a chave estrangeira da tabela de referência também é atualizada.<br /><br /> SQL_NO_ACTION: se uma atualização da chave primária da tabela referenciada causar uma "referência pendente" na tabela de referência (ou seja, as linhas na tabela de referência não teriam contrapartes na tabela referenciada), a atualização será rejeitada. Se uma atualização da chave estrangeira da tabela de referência introduzir um valor que não existe como um valor da chave primária da tabela referenciada, a atualização será rejeitada. (Essa ação é a mesma que a ação de SQL_RESTRICT no ODBC 2 *. x*.)<br /><br /> SQL_SET_NULL: quando uma ou mais linhas na tabela referenciada são atualizadas de forma que um ou mais componentes da chave primária sejam alterados, os componentes da chave estrangeira na tabela de referência que correspondem aos componentes alterados da chave primária são definidos como NULL em todas as linhas correspondentes da tabela de referência.<br /><br /> SQL_SET_DEFAULT: quando uma ou mais linhas na tabela referenciada são atualizadas de forma que um ou mais componentes da chave primária sejam alterados, os componentes da chave estrangeira na tabela de referência que correspondem aos componentes alterados da chave primária são definidos para os valores padrão aplicáveis em todas as linhas correspondentes da tabela de referência.<br /><br /> NULL se não for aplicável à fonte de dados.|  
|DELETE_RULE (ODBC 1,0)|11|Smallint|Ação a ser aplicada à chave estrangeira quando a operação SQL for **excluída**. Pode ter um dos valores a seguir. (A tabela referenciada é a tabela que tem a chave primária; a tabela de referência é a tabela que tem a chave estrangeira.)<br /><br /> SQL_CASCADE: quando uma linha na tabela referenciada é excluída, todas as linhas correspondentes nas tabelas de referência também são excluídas.<br /><br /> SQL_NO_ACTION: se uma exclusão de uma linha na tabela referenciada causar uma "referência pendente" na tabela de referência (ou seja, as linhas na tabela de referência não teriam contrapartes na tabela referenciada), a atualização será rejeitada. (Essa ação é a mesma que a ação de SQL_RESTRICT no ODBC 2 *. x*.)<br /><br /> SQL_SET_NULL: quando uma ou mais linhas na tabela referenciada são excluídas, cada componente da chave estrangeira da tabela de referência é definido como NULL em todas as linhas correspondentes da tabela de referência.<br /><br /> SQL_SET_DEFAULT: quando uma ou mais linhas na tabela referenciada são excluídas, cada componente da chave estrangeira da tabela de referência é definido como o padrão aplicável em todas as linhas correspondentes da tabela de referência.<br /><br /> NULL se não for aplicável à fonte de dados.|  
|FK_NAME (ODBC 2,0)|12|Varchar|Nome da chave estrangeira. NULL se não for aplicável à fonte de dados.|  
|PK_NAME (ODBC 2,0)|13|Varchar|Nome da chave primária. NULL se não for aplicável à fonte de dados.|  
|ADIAMENTO (ODBC 3,0)|14|Smallint|SQL_INITIALLY_DEFERRED, SQL_INITIALLY_IMMEDIATE SQL_NOT_DEFERRABLE.|  
  
## <a name="code-example"></a>Exemplo de código  
 Conforme ilustrado na tabela a seguir, este exemplo usa três tabelas, pedidos nomeados, linhas e clientes.  
  
|PEDIDOS|ALINHA|UTILIZAM|  
|------------|-----------|---------------|  
|ORDERID|ORDERID|CUSTID|  
|CUSTID|ALINHA|NAME|  
|OPENDATE|PARTID|CORRIGIR|  
|REPRESENTANTE|QUANTIDADE|TELEFONE|  
|STATUS|||  
  
 Na tabela ORDERs, CUSTid identifica o cliente para quem a venda foi feita. É uma chave estrangeira que se refere a CUSTid na tabela CUSTOMers.  
  
 Na tabela linhas, ORDERID identifica a ordem de venda com a qual o item de linha está associado. É uma chave estrangeira que se refere a ORDERID na tabela ORDERs.  
  
 Este exemplo chama **SQLPrimaryKeys** para obter a chave primária da tabela Orders. O conjunto de resultados terá uma linha; as colunas significativas são mostradas na tabela a seguir.  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|PEDIDOS|ORDERID|1|  
  
 Em seguida, o exemplo chama **SQLForeignKeys** para obter as chaves estrangeiras em outras tabelas que fazem referência à chave primária da tabela Orders. O conjunto de resultados terá uma linha; as colunas significativas são mostradas na tabela a seguir.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|PEDIDOS|CUSTID|ALINHA|CUSTID|1|  
  
 Por fim, o exemplo chama **SQLForeignKeys** para obter as chaves estrangeiras na tabela Orders que se referem às chaves primárias de outras tabelas. O conjunto de resultados terá uma linha; as colunas significativas são mostradas na tabela a seguir.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|UTILIZAM|CUSTID|PEDIDOS|CUSTID|1|  
  
```cpp  
#define TAB_LEN SQL_MAX_TABLE_NAME_LEN + 1  
#define COL_LEN SQL_MAX_COLUMN_NAME_LEN + 1  
  
LPSTR   szTable;              /* Table to display */  
  
UCHAR szPkTable[TAB_LEN];   /* Primary key table name */  
UCHAR szFkTable[TAB_LEN];   /* Foreign key table name */  
UCHAR szPkCol[COL_LEN];     /* Primary key column */  
UCHAR szFkCol[COL_LEN];     /* Foreign key column */  
  
SQLHSTMT      hstmt;  
SQLINTEGER    cbPkTable, cbPkCol, cbFkTable, cbFkCol, cbKeySeq;  
SQLSMALLINT   iKeySeq;  
SQLRETURN     retcode;  
  
// Bind the columns that describe the primary and foreign keys.  
// Ignore the table schema, name, and catalog for this example.  
  
SQLBindCol(hstmt, 3, SQL_C_CHAR, szPkTable, TAB_LEN, &cbPkTable);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, szPkCol, COL_LEN, &cbPkCol);  
SQLBindCol(hstmt, 5, SQL_C_SSHORT, &iKeySeq, TAB_LEN, &cbKeySeq);  
SQLBindCol(hstmt, 7, SQL_C_CHAR, szFkTable, TAB_LEN, &cbFkTable);  
SQLBindCol(hstmt, 8, SQL_C_CHAR, szFkCol, COL_LEN, &cbFkCol);  
  
strcpy_s(szTable, sizeof(szTable), "ORDERS");  
  
/* Get the names of the columns in the primary key. */  
  
retcode = SQLPrimaryKeys(hstmt,  
         NULL, 0,             /* Catalog name */  
         NULL, 0,             /* Schema name */  
         szTable, SQL_NTS);   /* Table name */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL SUCCESS_WITH_INFO)) {  
  
   /* Fetch and display the result set. This will be a list of the */  
   /* columns in the primary key of the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "Table: %s Column: %s Key Seq: %hd \n", szPkTable, szPkCol,  
      iKeySeq);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys that refer to ORDERS primary key.*/   
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,            /* Primary catalog */  
         NULL, 0,            /* Primary schema */  
         szTable, SQL_NTS,   /* Primary table */  
         NULL, 0,            /* Foreign catalog */  
         NULL, 0,            /* Foreign schema */  
         NULL, 0);           /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* foreign keys in other tables that refer to the ORDERS */  
/* primary key. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s ) <-- %-s ( %-s )\n", szPkTable,  
               szPkCol, szFkTable, szFkCol);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys in the ORDERS table. */  
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,             /* Primary catalog */  
         NULL, 0,             /* Primary schema */  
         NULL, 0,             /* Primary table */  
         NULL, 0,             /* Foreign catalog */  
         NULL, 0,             /* Foreign schema */  
         szTable, SQL_NTS);   /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* primary keys in other tables that are referred to by foreign */  
/* keys in the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s )--> %-s ( %-s )\n", szFkTable, szFkCol, szPkTable, szPkCol);  
}  
  
/* Free the hstmt. */  
SQLFreeStmt(hstmt, SQL_DROP);  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção somente de avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando as colunas de uma chave primária|[Função SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|Retornando índices e estatísticas de tabela|[Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
