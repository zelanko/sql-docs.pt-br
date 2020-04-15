---
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
ms.openlocfilehash: 5f2769fb378a5ee989fb6a0351537edb3de03469
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285856"
---
# <a name="sqlforeignkeys-function"></a>Função SQLForeignKeys
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **SQLForeignKeys** pode retornar:  
  
-   Uma lista de teclas estrangeiras na tabela especificada (colunas na tabela especificada que se referem a teclas primárias em outras tabelas).  
  
-   Uma lista de chaves estrangeiras em outras tabelas que se referem à chave principal na tabela especificada.  
  
 O driver retorna cada lista como resultado definido na declaração especificada.  
  
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
 [Entrada] Alça de declaração.  
  
 *PKCatalogName*  
 [Entrada] Nome do catálogo da tabela principal. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") denota as tabelas que não possuem catálogos. *PKCatalogName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *PKCatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *PKCatalogName* é um argumento comum; é tratado literalmente, e seu caso é significativo. Para obter mais informações, consulte [Argumentos em Funções de Catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento de **PKCatalogName*, em caracteres.  
  
 *PKSchemaNome*  
 [Entrada] Nome do esquema da tabela principal. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") denota as tabelas que não possuem esquemas. *PKSchemaName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID estiver definido como SQL_TRUE, *PKSchemaName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *PKSchemaName* é um argumento comum; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome2*  
 [Entrada] Comprimento de **PKSchemaName*, em caracteres.  
  
 *PKTableName*  
 [Entrada] Nome da mesa principal. *PKTableName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID estiver definido como SQL_TRUE, *PKTableName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *PKTableName* é um argumento comum; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome3*  
 [Entrada] Comprimento de **PKTableName*, em caracteres.  
  
 *FKCatalogName*  
 [Entrada] Nome do catálogo da tabela de chaves estrangeira. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") denota as tabelas que não possuem catálogos. *FKCatalogName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *FKCatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *FKCatalogName* é um argumento comum; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome4*  
 [Entrada] Comprimento de **FKCatalogName*, em caracteres.  
  
 *Nome de FKSchema*  
 [Entrada] Nome de esquema de mesa de chave estrangeira. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") denota as tabelas que não possuem esquemas. *FKSchemaName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *FKSchemaName* será tratado como um identificador e seu caso não é significativo. Se for SQL_FALSE, *FKSchemaName* é um argumento comum; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome5*  
 [Entrada] Comprimento de **FKSchemaName*, em caracteres.  
  
 *FKTableName*  
 [Entrada] Nome de mesa de chave estrangeira. *FKTableName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID estiver definido como SQL_TRUE, *FKTableName* será tratado como um identificador e seu caso não é significativo. Se for SQL_FALSE, *FKTableName* é um argumento comum; é tratado literalmente, e seu caso é significativo.  
  
 *NameLength6*  
 [Entrada] Comprimento de **FKTableName*, em caracteres.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLForeignKeys** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de controle de *declaração*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLForeignKeys** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|24.000|Estado de cursor inválido|Um cursor foi aberto no *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** foram chamados. Esse erro é devolvido pelo Gerenciador de driver se **o SQLFetch** ou **o SQLFetchScroll** não retornarem SQL_NO_DATA e forem devolvidos pelo driver se **o SQLFetch** ou **o SQLFetchScroll** retornarem SQL_NO_DATA.<br /><br /> Um cursor foi aberto no *StatementHandle,* mas **SQLFetch** ou **SQLFetchScroll** não foram chamados.|  
|40001|Falha na serialização|A transação foi revertida por causa de um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*e, em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY009|Uso inválido do ponteiro nulo|(DM) Os argumentos *PKTableName* e *FKTableName* foram ambos ponteiros nulos.<br /><br /> O SQL_ATTR_METADATA_ID atributo de declaração foi definido como SQL_TRUE, o argumento *FKCatalogName* ou *PKCatalogName* era um ponteiro nulo, e o SQL_CATALOG_NAME *InfoType* retorna que os nomes do catálogo são suportados.<br /><br /> (DM) O atributo de declaração SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *FKSchemaName*, *PKSchemaName,* *FKTableName*ou *PKTableName* foi um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função SQLForeignKeys foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor de um dos argumentos de comprimento do nome foi inferior a 0, mas não igual a SQL_NTS.|  
|||O valor de um dos argumentos de comprimento do nome excedeu o valor máximo de comprimento para o nome correspondente. (Veja "Comentários".)|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um nome de catálogo foi especificado e o driver ou fonte de dados não suporta catálogos.<br /><br /> Um nome de esquema foi especificado, e o driver ou fonte de dados não suporta esquemas.|  
|||A combinação das configurações atuais dos atributos de declaração SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não foi suportada pelo driver ou fonte de dados.<br /><br /> O atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de declaração SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o motorista não suporta marcadores.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo é definido através **de SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações sobre como as informações devolvidas por essa função podem ser usadas, consulte [Usos de Dados de Catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Se \* *PKTableName* contiver um nome de tabela, **SQLForeignKeys** retorna um conjunto de resultados que contém a chave principal da tabela especificada e todas as teclas estrangeiras que se referem a ela. A lista de chaves estrangeiras em outras tabelas não inclui chaves estrangeiras que apontam para restrições únicas na tabela especificada.  
  
 Se \* *FKTableName* contiver um nome de tabela, **SQLForeignKeys** retorna um conjunto de resultados que contém todas as teclas estrangeiras na tabela especificada que apontam para chaves primárias em outras tabelas e as teclas primárias nas outras tabelas a que se referem. A lista de chaves estrangeiras na tabela especificada não contém teclas estrangeiras que se referem a restrições únicas em outras tabelas.  
  
 Se \*tanto *PKTableName* quanto \* *FKTableName* contiverem nomes de tabela, **SQLForeignKeys** retorna as teclas estrangeiras na tabela especificada em \* *FKTableName* que se referem à chave principal da tabela especificada em **PKTableName*. Isso deve ser uma chave no máximo.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados das funções do catálogo oDBC, consulte [Funções de Catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLForeignKeys** retorna os resultados como um conjunto de resultados padrão. Se as chaves estrangeiras associadas a uma chave primária forem solicitadas, o conjunto de resultados será ordenado por FKTABLE_CAT, FKTABLE_SCHEM, FKTABLE_NAME e KEY_SEQ. Se as chaves primárias associadas a uma chave estrangeira forem solicitadas, o conjunto de resultados será ordenado por PKTABLE_CAT, PKTABLE_SCHEM, PKTABLE_NAME e KEY_SEQ. A tabela a seguir lista as colunas no conjunto de resultados.  
  
 Os comprimentos das colunas VARCHAR não são mostrados na tabela; os comprimentos reais dependem da fonte de dados. Para determinar os comprimentos reais do PKTABLE_CAT ou FKTABLE_CAT, PKTABLE_SCHEM ou FKTABLE_SCHEM, PKTABLE_NAME ou FKTABLE_NAME e colunas de PKCOLUMN_NAME ou FKCOLUMN_NAME, um aplicativo pode ligar para **o SQLGetInfo** com as opções de SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
 As seguintes colunas foram renomeadas para ODBC 3 *.x.* As alterações de nome da coluna não afetam a compatibilidade retrógrada porque os aplicativos se ligam por número de coluna.  
  
|Coluna ODBC 2.0|Coluna ODBC 3 *.x*|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 14 (OBSERVAÇÕES) podem ser definidas pelo driver. Um aplicativo deve ter acesso a colunas específicas do driver, contando abaixo do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [Dados Retornados por Funções de Catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|Nome do catálogo da tabela principal; NULL se não aplicável à fonte de dados. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aquelas tabelas que não possuem catálogos.|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome do esquema da tabela principal; NULL se não aplicável à fonte de dados. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aquelas tabelas que não possuem esquemas.|  
|PKTABLE_NAME (ODBC 1.0)|3|Varchar não É NULO|Nome da mesa principal.|  
|PKCOLUMN_NAME (ODBC 1.0)|4|Varchar não É NULO|Nome da coluna principal. O driver retorna uma seqüência vazia para uma coluna que não tem um nome.|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|Nome do catálogo da tabela de chaves estrangeira; NULL se não aplicável à fonte de dados. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aquelas tabelas que não possuem catálogos.|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|Nome do esquema da tabela de chave estrangeira; NULL se não aplicável à fonte de dados. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aquelas tabelas que não possuem esquemas.|  
|FKTABLE_NAME (ODBC 1.0)|7|Varchar não É NULO|Nome de mesa de chave estrangeira.|  
|FKCOLUMN_NAME (ODBC 1.0)|8|Varchar não É NULO|Nome da coluna de chave estrangeira. O driver retorna uma seqüência vazia para uma coluna que não tem um nome.|  
|KEY_SEQ (ODBC 1.0)|9|Smallint não NULL|Número da seqüência da coluna na tecla (começando com 1).|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|Ação a ser aplicada à chave estrangeira quando a operação SQL é **UPDATE**. Pode ter um dos seguintes valores. (A tabela referenciada é a tabela que tem a chave principal; a tabela de referência é a tabela que tem a chave estrangeira.)<br /><br /> SQL_CASCADE: Quando a chave primária da tabela referenciada é atualizada, a chave estrangeira da tabela de referência também é atualizada.<br /><br /> SQL_NO_ACTION: Se uma atualização da chave primária da tabela mencionada causaria uma "referência pendente" na tabela de referência (ou seja, as linhas na tabela de referência não teriam contrapartes na tabela referenciada), a atualização seria rejeitada. Se uma atualização da chave estrangeira da tabela de referência introduzir um valor que não existe como valor da chave primária da tabela referenciada, a atualização será rejeitada. (Esta ação é a mesma que a ação SQL_RESTRICT no ODBC 2 *.x*.)<br /><br /> SQL_SET_NULL: Quando uma ou mais linhas na tabela referenciada são atualizadas de forma que um ou mais componentes da tecla primária sejam alterados, os componentes da tecla estrangeira na tabela de referência que correspondem aos componentes alterados da tecla primária são definidos como NULAS em todas as linhas correspondentes da tabela de referência.<br /><br /> SQL_SET_DEFAULT: Quando uma ou mais linhas na tabela referenciada são atualizadas de forma que um ou mais componentes da chave primária sejam alterados, os componentes da tecla estrangeira na tabela de referência que correspondem aos componentes alterados da tecla primária são definidos para os valores padrão aplicáveis em todas as linhas correspondentes da tabela de referência.<br /><br /> NULL se não aplicável à fonte de dados.|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|Ação a ser aplicada à chave estrangeira quando a operação SQL é **DELETE**. Pode ter um dos seguintes valores. (A tabela referenciada é a tabela que tem a chave principal; a tabela de referência é a tabela que tem a chave estrangeira.)<br /><br /> SQL_CASCADE: Quando uma linha na tabela referenciada é excluída, todas as linhas correspondentes nas tabelas de referência também são excluídas.<br /><br /> SQL_NO_ACTION: Se uma exclusão de uma linha na tabela mencionada causaria uma "referência pendente" na tabela de referência (ou seja, as linhas na tabela de referência não teriam contrapartes na tabela referencial), a atualização seria rejeitada. (Esta ação é a mesma que a ação SQL_RESTRICT no ODBC 2 *.x*.)<br /><br /> SQL_SET_NULL: Quando uma ou mais linhas na tabela referenciada são excluídas, cada componente da tecla estrangeira da tabela de referência é definido como NULO em todas as linhas correspondentes da tabela de referência.<br /><br /> SQL_SET_DEFAULT: Quando uma ou mais linhas na tabela referenciada são excluídas, cada componente da tecla estrangeira da tabela de referência é definido como padrão aplicável em todas as linhas correspondentes da tabela de referência.<br /><br /> NULL se não aplicável à fonte de dados.|  
|FK_NAME (ODBC 2.0)|12|Varchar|Nome de chave estrangeira. NULL se não aplicável à fonte de dados.|  
|PK_NAME (ODBC 2.0)|13|Varchar|Nome principal. NULL se não aplicável à fonte de dados.|  
|DIFERIMENTO (ODBC 3.0)|14|Smallint|SQL_INITIALLY_DEFERRED, SQL_INITIALLY_IMMEDIATE, SQL_NOT_DEFERRABLE.|  
  
## <a name="code-example"></a>Exemplo de código  
 Conforme ilustrado na tabela a seguir, este exemplo usa três tabelas, chamadas ORDERS, LINES e CUSTOMERS.  
  
|PEDIDOS|Linhas|Clientes|  
|------------|-----------|---------------|  
|Orderid|Orderid|CUSTID|  
|CUSTID|Linhas|NAME|  
|DATA DE ABERTURA|PARTID|Endereço|  
|Vendedor|Quantidade|TELEFONE|  
|STATUS|||  
  
 Na tabela ORDERS, custid identifica o cliente a quem a venda foi feita. É uma chave estrangeira que se refere a CUSTID na tabela CLIENTES.  
  
 Na tabela LINHAS, o ORDERID identifica a ordem de venda com a qual o item de linha está associado. É uma chave estrangeira que se refere ao ORDERID na tabela ORDERS.  
  
 Este exemplo chama **SQLPrimaryKeys** para obter a chave principal da tabela ORDERS. O conjunto de resultados terá uma linha; as colunas significativas são mostradas na tabela a seguir.  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|PEDIDOS|Orderid|1|  
  
 Em seguida, o exemplo chama **SQLForeignKeys** para obter as teclas estrangeiras em outras tabelas que fazem referência à chave principal da tabela ORDERS. O conjunto de resultados terá uma linha; as colunas significativas são mostradas na tabela a seguir.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|PEDIDOS|CUSTID|Linhas|CUSTID|1|  
  
 Finalmente, o exemplo chama **SQLForeignKeys** para obter as teclas estrangeiras na tabela ORDERS que se referem às teclas primárias de outras tabelas. O conjunto de resultados terá uma linha; as colunas significativas são mostradas na tabela a seguir.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|Clientes|CUSTID|PEDIDOS|CUSTID|1|  
  
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
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscar uma única linha ou um bloco de dados em uma direção somente para a frente|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando as colunas de uma chave primária|[Função SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|Estatísticas e índices da tabela de retorno|[Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
