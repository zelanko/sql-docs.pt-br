---
title: Função SQLColumns | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumns
helpviewer_keywords:
- SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36293c1f2393e9a57351fc8cd19dcc6e3338f5cc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301252"
---
# <a name="sqlcolumns-function"></a>Função SQLColumns
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: Open Group  
  
 **Resumo**  
 **SQLColumns** retorna a lista de nomes de coluna sem tabelas especificadas. O driver retorna essas informações como resultado definido no *StatementHandle*especificado .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLColumns(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      ColumnName,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *Catalogname*  
 [Entrada] Nome do catálogo. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") indica as tabelas que não possuem catálogos. *CatalogName* não pode conter um padrão de pesquisa de seqüência.  
  
> [!NOTE]  
>  Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *o CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; é tratado literalmente, e seu caso é significativo. Para obter mais informações, consulte [Argumentos em Funções de Catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *Schemaname*  
 [Entrada] Padrão de busca de cordas para nomes de esquemas. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") indica aquelas tabelas que não possuem esquemas.  
  
> [!NOTE]  
>  Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *O SchemaName* é tratado como um identificador e seu caso não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *Tablename*  
 [Entrada] Padrão de pesquisa de cordas para nomes de tabela.  
  
> [!NOTE]  
>  Se o atributo de declaração SQL_ATTR_METADATA_ID estiver definido como SQL_TRUE, *O Nome da Tabela* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *TableName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome3*  
 [Entrada] Comprimento em caracteres de **TableName*.  
  
 *ColumnName*  
 [Entrada] Padrão de pesquisa de cordas para nomes de colunas.  
  
> [!NOTE]  
>  Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *O Nome da Coluna* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *ColumnName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome4*  
 [Entrada] Comprimento em caracteres de **ColumnName*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLColumns** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLColumns** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|24.000|Estado de cursor inválido|Um cursor foi aberto no *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** foram chamados. Esse erro é devolvido pelo Gerenciador de driver se **o SQLFetch** ou **o SQLFetchScroll** não retornarem SQL_NO_DATA e forem devolvidos pelo driver se **o SQLFetch** ou **o SQLFetchScroll** retornarem SQL_NO_DATA.<br /><br /> Um cursor foi aberto no *StatementHandle,* mas **SQLFetch** ou **SQLFetchScroll** não foram chamados.|  
|40001|Falha na serialização|A transação foi revertida por causa de um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY009|Uso inválido do ponteiro nulo|O SQL_ATTR_METADATA_ID atributo de declaração foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes do catálogo são suportados.<br /><br /> (DM) O atributo de declaração SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName,* *TableName*ou *ColumnName* era um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLColumns** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor de um dos argumentos de comprimento do nome foi inferior a 0, mas não igual a SQL_NTS.|  
|||O valor de um dos argumentos de comprimento do nome excedeu o valor máximo de comprimento para o catálogo ou nome correspondente. O comprimento máximo de cada catálogo ou nome pode ser obtido ligando para **SQLGetInfo** com os valores do *InfoType.* (Veja "Comentários".)|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um nome de catálogo foi especificado e o driver ou fonte de dados não suporta catálogos.<br /><br /> Um nome de esquema foi especificado, e o driver ou fonte de dados não suporta esquemas.<br /><br /> Um padrão de pesquisa de seqüência foi especificado para o nome do esquema, nome da tabela ou nome da coluna, e a fonte de dados não suporta padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de declaração SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não foi suportada pelo driver ou fonte de dados.<br /><br /> O atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de declaração SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o motorista não suporta marcadores.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo é definido através **de SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Essa função normalmente é usada antes da execução da declaração para recuperar informações sobre colunas para uma tabela ou tabelas do catálogo da fonte de dados. **SQLColumns** podem ser usados para recuperar dados para todos os tipos de itens retornados pelo **SQLTables**. Além das tabelas base, isso pode incluir (mas não se limita a) visualizações, sinônimos, tabelas de sistema e assim por diante. Em contraste, as funções **SQLColAttribute** e **SQLDescribeCol** descrevem as colunas em um conjunto de resultados e a função **SQLNumResultCols** retorna o número de colunas em um conjunto de resultados. Para obter mais informações, consulte [Usos de Dados de Catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados das funções do catálogo oDBC, consulte [Funções de Catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **O SQLColumns** retorna os resultados como um conjunto de resultados padrão, ordenado por TABLE_CAT, TABLE_SCHEM, TABLE_NAME e ORDINAL_POSITION.  
  
> [!NOTE]  
>  Quando um aplicativo funciona com um ODBC 2. *x* driver, nenhuma ORDINAL_POSITION coluna é devolvida no conjunto de resultados. Como resultado, ao trabalhar com ODBC 2. *x* drivers, a ordem das colunas na lista de colunas retornadas por **SQLColumns** não é necessariamente a mesma que a ordem das colunas retornadas quando o aplicativo executa uma declaração SELECT em todas as colunas nessa tabela.  
  
> [!NOTE]  
>  **SQLColumns** pode não retornar todas as colunas. Por exemplo, um driver pode não retornar informações sobre pseudo-colunas, como o Oracle ROWID. Os aplicativos podem usar qualquer coluna válida, quer seja devolvida por **SQLColumns**.  
>   
>  Algumas colunas que podem ser devolvidas pelo **SQLStatistics** não são devolvidas por **SQLColumns**. Por exemplo, **SQLColumns** não retorna as colunas em um índice criado sobre uma expressão ou filtro, como SALÁRIO + BENEFÍCIOS ou DEPT = 0012.  
  
 Os comprimentos das colunas VARCHAR não são mostrados na tabela; os comprimentos reais dependem da fonte de dados. Para determinar os comprimentos reais das colunas de TABLE_CAT, TABLE_SCHEM, TABLE_NAME e COLUMN_NAME, um aplicativo pode chamar **o SQLGetInfo** com as opções de SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
 As seguintes colunas foram renomeadas para ODBC 3. *x*. As alterações de nome da coluna não afetam a compatibilidade retrógrada porque os aplicativos se ligam por número de coluna.  
  
|Coluna ODBC 2.0|ODBC 3. *x* coluna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 As seguintes colunas foram adicionadas ao conjunto de resultados retornado por **SQLColumns** para ODBC 3. *x:*  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 18 (IS_NULLABLE) podem ser definidas pelo driver. Um aplicativo deve ter acesso a colunas específicas do driver, contando abaixo do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [Dados Retornados por Funções de Catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Coluna<br /><br /> número|Tipo de dados|Comentários|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nome do catálogo; NULL se não aplicável à fonte de dados. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aquelas tabelas que não possuem catálogos.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome do esquema; NULL se não aplicável à fonte de dados. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aquelas tabelas que não possuem esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar não É NULO|Nome da tabela.|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar não É NULO|Nome da coluna. O driver retorna uma seqüência vazia para uma coluna que não tem um nome.|  
|DATA_TYPE (ODBC 1.0)|5|Smallint não NULL|Tipo de dados SQL. Isso pode ser um tipo de dados SQL ODBC ou um tipo de dados SQL específico para driver. Para os tipos de dados de data e intervalo, esta coluna retorna o tipo de dados concisos (como SQL_TYPE_DATE ou SQL_INTERVAL_YEAR_TO_MONTH, em vez do tipo de dados não concisos, como SQL_DATETIME ou SQL_INTERVAL). Para obter uma lista de tipos de dados SQL odbc válidos, consulte [Tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no apêndice D: Tipos de dados. Para obter informações sobre os tipos de dados SQL específicos do driver, consulte a documentação do motorista.<br /><br /> Os tipos de dados retornaram para ODBC 3. *x* e ODBC 2. *x* aplicações podem ser diferentes. Para obter mais informações, consulte [Retrocompatibilidade e Conformidade de Padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).|  
|TYPE_NAME (ODBC 1.0)|6|Varchar não É NULO|Nome do tipo de dados dependente da fonte de dados; por exemplo, "CHAR", "VARCHAR", "MONEY", "LONG VARBINAR" ou "CHAR ( ) FOR BIT DATA".|  
|COLUMN_SIZE (ODBC 1.0)|7|Integer|Se DATA_TYPE for SQL_CHAR ou SQL_VARCHAR, esta coluna contém o comprimento máximo em caracteres da coluna. Para os tipos de dados de data-hora, este é o número total de caracteres necessários para exibir o valor quando ele é convertido em caracteres. Para tipos de dados numéricos, este é o número total de dígitos ou o número total de bits permitidos na coluna, de acordo com a coluna NUM_PREC_RADIX. Para tipos de dados de intervalo, este é o número de caracteres na representação de caracteres do intervalo literal (conforme definido pela precisão de intervalo de líder, consulte [Interval Data Type Length](../../../odbc/reference/appendixes/interval-data-type-length.md) in Apêndice D: Data Types). Para obter mais informações, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no apêndice D: Tipos de dados.|  
|BUFFER_LENGTH (ODBC 1.0)|8|Integer|O comprimento em bytes de dados transferidos em uma operação SQLGetData, SQLFetch ou SQLFetchScroll se SQL_C_DEFAULT for especificada. Para dados numéricos, esse tamanho pode diferir do tamanho dos dados armazenados na fonte de dados. Esse valor pode diferir da coluna COLUMN_SIZE para dados de caracteres. Para obter mais informações sobre o comprimento, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do Octeto de Transferência e Tamanho do Display](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: Tipos de dados.|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|O número total de dígitos significativos à direita do ponto decimal. Para SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP, esta coluna contém o número de dígitos no componente de segundos fracionados. Para os outros tipos de dados, estes são os dígitos decimais da coluna na fonte de dados. Para tipos de dados de intervalo que contêm um componente de tempo, esta coluna contém o número de dígitos à direita do ponto decimal (segundos fracionados). Para tipos de dados de intervalo que não contenham um componente de tempo, esta coluna é 0. Para obter mais informações sobre dígitos decimais, consulte Tamanho da [coluna, Dígitos Decimais, Comprimento do Octeto de Transferência e Tamanho de Exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: Tipos de dados. NULL é devolvido para tipos de dados quando DECIMAL_DIGITS não é aplicável.|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|Para tipos de dados numéricos, 10 ou 2. Se for 10, os valores em COLUMN_SIZE e DECIMAL_DIGITS dão o número de dígitos decimais permitidos para a coluna. Por exemplo, uma coluna DECIMAL (12,5) retornaria um NUM_PREC_RADIX de 10, um COLUMN_SIZE de 12 e um DECIMAL_DIGITS de 5; uma coluna FLOAT poderia retornar um NUM_PREC_RADIX de 10, um COLUMN_SIZE de 15, e um DECIMAL_DIGITS de NULL.<br /><br /> Se for 2, os valores em COLUMN_SIZE e DECIMAL_DIGITS dão o número de bits permitidos na coluna. Por exemplo, uma coluna FLOAT poderia retornar um RADIX de 2, um COLUMN_SIZE de 53 e um DECIMAL_DIGITS de NULL.<br /><br /> NULL é devolvido para tipos de dados quando NUM_PREC_RADIX não é aplicável.|  
|ANULADO (ODBC 1.0)|11|Smallint não NULL|SQL_NO_NULLS se a coluna não pudesse incluir valores NULL.<br /><br /> SQL_NULLABLE se a coluna aceitar valores NULOS.<br /><br /> SQL_NULLABLE_UNKNOWN se não se sabe se a coluna aceita valores NULOS.<br /><br /> O valor devolvido para esta coluna difere do valor devolvido para a coluna IS_NULLABLE. A coluna NULLABLE indica com certeza que uma coluna pode aceitar NULLs, mas não pode indicar com certeza que uma coluna não aceita NULLs. A coluna IS_NULLABLE indica com certeza que uma coluna não pode aceitar NULLs, mas não pode indicar com certeza que uma coluna aceita NULLs.|  
|OBSERVAÇÕES (ODBC 1.0)|12|Varchar|Uma descrição da coluna.|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|O valor padrão da coluna. O valor nesta coluna deve ser interpretado como uma seqüência se estiver incluído entre aspas.<br /><br /> Se NULL foi especificado como o valor padrão, esta coluna será a palavra NULL, não incluída entre aspas. Se o valor padrão não puder ser representado sem truncação, esta coluna contém TRUNCATED, sem fechar aspas únicas. Se nenhum valor padrão foi especificado, esta coluna será NULL.<br /><br /> O valor de COLUMN_DEF pode ser usado na geração de uma nova definição de coluna, exceto quando contém o valor TRUNCATED.|  
|SQL_DATA_TYPE (ODBC 3.0)|14|Smallint não NULL|Tipo de dados SQL, como aparece no campo de registro SQL_DESC_TYPE no IRD. Isso pode ser um tipo de dados SQL ODBC ou um tipo de dados SQL específico para driver. Esta coluna é a mesma da coluna DATA_TYPE, exceto para os tipos de dados de data e intervalo. Esta coluna retorna o tipo de dados não concisoso (como SQL_DATETIME ou SQL_INTERVAL), em vez do tipo de dados concisos (como SQL_TYPE_DATE ou SQL_INTERVAL_YEAR_TO_MONTH) para tipos de dados de data e intervalo. Se esta coluna retornar SQL_DATETIME ou SQL_INTERVAL, o tipo de dados específico pode ser determinado a partir da coluna SQL_DATETIME_SUB. Para obter uma lista de tipos de dados SQL odbc válidos, consulte [Tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no apêndice D: Tipos de dados. Para obter informações sobre os tipos de dados SQL específicos do driver, consulte a documentação do motorista.<br /><br /> Os tipos de dados retornaram para ODBC 3. *x* e ODBC 2. *x* aplicações podem ser diferentes. Para obter mais informações, consulte [Retrocompatibilidade e Conformidade de Padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|O código de subtipo para os tipos de dados de data e intervalo. Para outros tipos de dados, esta coluna retorna um NULL. Para obter mais informações sobre subcódigos de data e intervalo, consulte "SQL_DESC_DATETIME_INTERVAL_CODE" no [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|Integer|O comprimento máximo em bytes de uma coluna de tipo de dados de caracteres ou binários. Para todos os outros tipos de dados, esta coluna retorna um NULL.|  
|ORDINAL_POSITION (ODBC 3.0)|17|Integer não NULL|A posição ordinal da coluna na tabela. A primeira coluna na tabela é o número 1.|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|"NÃO" se a coluna não incluir NULLs.<br /><br /> "SIM" se a coluna pudesse incluir NULLs.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS em conformidade com ISO SQL não pode retornar uma cadeia de caracteres vazia.<br /><br /> O valor devolvido para esta coluna difere do valor devolvido para a coluna NULLABLE. (Veja a descrição da coluna NULLABLE.)|  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo declara buffers para o conjunto de resultados retornado por **SQLColumns**. Ele chama **SQLColumns** para retornar um conjunto de resultados que descreve cada coluna na tabela EMPLOYEE. Em seguida, ele chama **SQLBindCol** para vincular as colunas no conjunto de resultados aos buffers. Finalmente, o aplicativo busca cada linha de dados com **SQLFetch** e processa-os.  
  
```cpp  
// SQLColumns_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
// Declare buffers for result set data  
SQLCHAR szSchema[STR_LEN];  
SQLCHAR szCatalog[STR_LEN];  
SQLCHAR szColumnName[STR_LEN];  
SQLCHAR szTableName[STR_LEN];  
SQLCHAR szTypeName[STR_LEN];  
SQLCHAR szRemarks[REM_LEN];  
SQLCHAR szColumnDefault[STR_LEN];  
SQLCHAR szIsNullable[STR_LEN];  
  
SQLINTEGER ColumnSize;  
SQLINTEGER BufferLength;  
SQLINTEGER CharOctetLength;  
SQLINTEGER OrdinalPosition;  
  
SQLSMALLINT DataType;  
SQLSMALLINT DecimalDigits;  
SQLSMALLINT NumPrecRadix;  
SQLSMALLINT Nullable;  
SQLSMALLINT SQLDataType;  
SQLSMALLINT DatetimeSubtypeCode;  
  
SQLHSTMT hstmt = NULL;  
  
// Declare buffers for bytes available to return  
SQLINTEGER cbCatalog;  
SQLINTEGER cbSchema;  
SQLINTEGER cbTableName;  
SQLINTEGER cbColumnName;  
SQLINTEGER cbDataType;  
SQLINTEGER cbTypeName;  
SQLINTEGER cbColumnSize;  
SQLLEN cbBufferLength;  
SQLINTEGER cbDecimalDigits;  
SQLINTEGER cbNumPrecRadix;  
SQLINTEGER cbNullable;  
SQLINTEGER cbRemarks;  
SQLINTEGER cbColumnDefault;  
SQLINTEGER cbSQLDataType;  
SQLINTEGER cbDatetimeSubtypeCode;  
SQLINTEGER cbCharOctetLength;  
SQLINTEGER cbOrdinalPosition;  
SQLINTEGER cbIsNullable;  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retcode = SQLColumns(hstmt, NULL, 0, NULL, 0, (SQLCHAR*)"CUSTOMERS", SQL_NTS, NULL, 0);  
  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      // Bind columns in result set to buffers  
      SQLBindCol(hstmt, 1, SQL_C_CHAR, szCatalog, STR_LEN,&cbCatalog);  
      SQLBindCol(hstmt, 2, SQL_C_CHAR, szSchema, STR_LEN, &cbSchema);  
      SQLBindCol(hstmt, 3, SQL_C_CHAR, szTableName, STR_LEN,&cbTableName);  
      SQLBindCol(hstmt, 4, SQL_C_CHAR, szColumnName, STR_LEN, &cbColumnName);  
      SQLBindCol(hstmt, 5, SQL_C_SSHORT, &DataType, 0, &cbDataType);  
      SQLBindCol(hstmt, 6, SQL_C_CHAR, szTypeName, STR_LEN, &cbTypeName);  
      SQLBindCol(hstmt, 7, SQL_C_SLONG, &ColumnSize, 0, &cbColumnSize);  
      SQLBindCol(hstmt, 8, SQL_C_SLONG, &BufferLength, 0, &cbBufferLength);  
      SQLBindCol(hstmt, 9, SQL_C_SSHORT, &DecimalDigits, 0, &cbDecimalDigits);  
      SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix, 0, &cbNumPrecRadix);  
      SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable, 0, &cbNullable);  
      SQLBindCol(hstmt, 12, SQL_C_CHAR, szRemarks, REM_LEN, &cbRemarks);  
      SQLBindCol(hstmt, 13, SQL_C_CHAR, szColumnDefault, STR_LEN, &cbColumnDefault);  
      SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType, 0, &cbSQLDataType);  
      SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode, 0, &cbDatetimeSubtypeCode);  
      SQLBindCol(hstmt, 16, SQL_C_SLONG, &CharOctetLength, 0, &cbCharOctetLength);  
      SQLBindCol(hstmt, 17, SQL_C_SLONG, &OrdinalPosition, 0, &cbOrdinalPosition);  
      SQLBindCol(hstmt, 18, SQL_C_CHAR, szIsNullable, STR_LEN, &cbIsNullable);  
  
      while (SQL_SUCCESS == retcode) {  
         retcode = SQLFetch(hstmt);  
         /*  
         if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // show_error();  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // Process fetched data  
         else  
            break;  
        */  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolvendo privilégios para uma coluna ou colunas|[Função SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Colunas de retorno que identificam exclusivamente uma linha ou colunas atualizadas automaticamente por uma transação|[Função SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|Estatísticas e índices da tabela de retorno|[Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Retornando uma lista de tabelas em uma fonte de dados|[Função SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
|Devolvendo privilégios para uma tabela ou tabela|[Função SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
