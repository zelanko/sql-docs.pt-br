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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51b14014853e0ccb91293097fd3aa81c1edcb2ae
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207735"
---
# <a name="sqlcolumns-function"></a>Função SQLColumns
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: Open Group  
  
 **Resumo**  
 **SQLColumns** retorna a lista de nomes de colunas em tabelas especificadas. O driver retorna essas informações como um conjunto de resultados em especificado *StatementHandle*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Identificador de instrução.  
  
 *CatalogName*  
 [Entrada] Nome do catálogo. Se um driver compatível com catálogos para algumas tabelas, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica as tabelas que não têm catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
> [!NOTE]  
>  Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Padrão de pesquisa de cadeia de caracteres para nomes de esquema. Se um driver compatível com esquemas para algumas tabelas, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica as tabelas que não tem esquemas.  
  
> [!NOTE]  
>  Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor padrão; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Padrão de pesquisa de cadeia de caracteres para nomes de tabela.  
  
> [!NOTE]  
>  Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *TableName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *TableName* é um argumento de valor padrão; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength3*  
 [Entrada] Comprimento em caracteres de **TableName*.  
  
 *ColumnName*  
 [Entrada] Padrão de pesquisa de cadeia de caracteres para nomes de coluna.  
  
> [!NOTE]  
>  Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *ColumnName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *ColumnName* é um argumento de valor padrão; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength4*  
 [Entrada] Comprimento em caracteres de **ColumnName*.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLColumns** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLColumns** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|Um cursor foi aberto sobre o *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada. Esse erro é retornado pelo Gerenciador de Driver, se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tem retornar SQL_NO_DATA.<br /><br /> Um cursor foi aberto sobre o *StatementHandle* mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão desconhecida de declaração|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|O atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o *CatalogName* argumento era um ponteiro nulo e o SQL_CATALOG_NAME *tipo de informação* retorna nomes de catálogo têm suporte.<br /><br /> (DM) o atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE e o *SchemaName*, *TableName*, ou *ColumnName* argumento é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLColumns** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor de um dos argumentos de comprimento do nome da era menor que 0 mas não iguais a SQL_NTS.|  
|||O valor de um dos argumentos de comprimento de nome excedeu o valor de comprimento máximo para o nome ou o catálogo correspondente. O comprimento máximo de cada catálogo ou o nome pode ser obtido chamando **SQLGetInfo** com o *tipo de informação* valores. (Consulte "Comentários".)|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Foi especificado um nome de catálogo, e o driver ou fonte de dados não oferece suporte a catálogos.<br /><br /> Foi especificado um nome de esquema e o driver ou fonte de dados não oferece suporte a esquemas.<br /><br /> Um padrão de pesquisa de cadeia de caracteres foi especificado para o nome do esquema, o nome da tabela ou o nome da coluna e a fonte de dados não dá suporte a padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era compatível com a driver ou fonte de dados.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo SQL_ATTR_CURSOR_TYPE de instrução foi definido como um tipo de cursor para o qual o driver não oferece suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornou o conjunto de resultados. O período de tempo limite é definido por meio **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Essa função normalmente é usada antes da execução de instrução para recuperar informações sobre colunas de uma tabela ou tabelas de catálogo da fonte de dados. **SQLColumns** pode ser usado para recuperar dados para todos os tipos de itens retornados pela **SQLTables**. Além das tabelas base, isso pode incluir (mas não está limitado a) exibições, sinônimos, tabelas do sistema e assim por diante. Por outro lado, as funções **SQLColAttribute** e **SQLDescribeCol** descrevem as colunas em um conjunto de resultados e a função **SQLNumResultCols** retorna o número de colunas em um conjunto de resultados. Para obter mais informações, consulte [usa do catálogo de dados](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, os argumentos e os dados retornados de funções de catálogo ODBC, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLColumns** retorna os resultados como um conjunto de resultados padrão, ordenado por TABLE_CAT, por TABLE_SCHEM, TABLE_NAME e ORDINAL_POSITION.  
  
> [!NOTE]  
>  Quando o aplicativo funciona com um ODBC 2. *x* driver, nenhuma coluna ORDINAL_POSITION é retornada no conjunto de resultados. Como resultado, ao trabalhar com ODBC 2. *x* drivers, a ordem das colunas na lista de colunas retornado pelo **SQLColumns** não é necessariamente o mesmo que a ordem das colunas retornado quando o aplicativo executa uma instrução SELECT em todas as colunas nessa tabela.  
  
> [!NOTE]  
>  **SQLColumns** não pode retornar todas as colunas. Por exemplo, um driver pode não retornar informações sobre colunas pseudo, como Oracle ROWID. Os aplicativos podem usar qualquer coluna válida, se ele é retornado por **SQLColumns**.  
>   
>  Algumas colunas que podem ser retornadas pelo **SQLStatistics** não são retornados pelo **SQLColumns**. Por exemplo, **SQLColumns** não retorna as colunas em um índice criado em uma expressão ou um filtro, como o SALÁRIO + benefícios ou DEPT = 0012.  
  
 Os comprimentos das colunas VARCHAR não são mostrados na tabela; os comprimentos reais dependem da fonte de dados. Para determinar os comprimentos reais das colunas TABLE_CAT, por TABLE_SCHEM, TABLE_NAME e nome da coluna, um aplicativo pode chamar **SQLGetInfo** com o SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN, e opções de SQL_MAX_COLUMN_NAME_LEN.  
  
 As seguintes colunas foram renomeadas para ODBC 3. *x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores, porque aplicativos associar por número de coluna.  
  
|Coluna de ODBC 2.0|ODBC 3. *x* coluna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 As colunas a seguir foram adicionadas ao conjunto de resultados retornado por **SQLColumns** para ODBC 3. *x*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 18 (IS_NULLABLE) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas do driver, contagem regressiva do final do conjunto em vez de especificar uma posição ordinal explícita de resultados. Para obter mais informações, consulte [dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|coluna<br /><br /> number|Tipo de dados|Comentários|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nome do catálogo; NULL se não for aplicável à fonte de dados. Se um driver compatível com catálogos para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm catálogos.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome do esquema; NULL se não for aplicável à fonte de dados. Se um driver compatível com esquemas para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não tem esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar não nulo|Nome da tabela.|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar não nulo|Nome da coluna. O driver retornará uma cadeia de caracteres vazia para uma coluna que não tem um nome.|  
|DATA_TYPE (ODBC 1.0)|5|Smallint não NULL|Tipo de dados SQL. Isso pode ser um tipo de dados SQL ODBC ou um tipo de dados SQL específica do driver. Para tipos de dados de data e hora e intervalo, esta coluna retorna o tipo de dados concisa (como SQL_TYPE_DATE ou SQL_INTERVAL_YEAR_TO_MONTH, em vez do tipo de dados nonconcise como SQL_DATETIME ou SQL_INTERVAL). Para obter uma lista dos tipos de dados SQL ODBC válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice d: Tipos de dados. Para obter informações sobre tipos de dados SQL específico do driver, consulte a documentação do driver.<br /><br /> Os tipos de dados retornados para o ODBC 3. *x* e o ODBC 2. *x* aplicativos podem ser diferentes. Para obter mais informações, consulte [compatibilidade com versões anteriores e em conformidade com padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).|  
|TYPE_NAME (ODBC 1.0)|6|Varchar não nulo|Nome do tipo de dados dependente da fonte de dados; Por exemplo, "CHAR", "VARCHAR", "Dinheiro", "Longo VARBINAR" ou "CHAR () para dados BIT".|  
|COLUMN_SIZE (ODBC 1.0)|7|Integer|Se o DATA_TYPE é SQL_CHAR ou SQL_VARCHAR, esta coluna contém o comprimento máximo em caracteres da coluna. Para tipos de dados de data e hora, isso é o número total de caracteres necessários para exibir o valor quando ele é convertido em caracteres. Para tipos de dados numéricos, isso é o número total de dígitos ou o número total de bits permitidos na coluna, de acordo com a coluna NUM_PREC_RADIX. Para tipos de dados de intervalo, este é o número de caracteres na representação de caractere do intervalo de literal (conforme definido pelo intervalo de precisão inicial, consulte [comprimento do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md) no Apêndice d: Tipos de dados). Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: Tipos de dados.|  
|BUFFER_LENGTH (ODBC 1.0)|8|Integer|O comprimento em bytes dos dados transferidos em uma operação de SQLGetData, SQLFetch ou SQLFetchScroll se SQL_C_DEFAULT for especificado. Dados numéricos, esse tamanho pode diferir do tamanho dos dados armazenados na fonte de dados. Esse valor pode diferir da coluna COLUMN_SIZE para dados de caracteres. Para obter mais informações sobre o tamanho, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: Tipos de dados.|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|O número total de dígitos significativos para a direita da vírgula decimal. Para SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP, esta coluna contém o número de dígitos no componente de segundos fracionários. Para outros tipos de dados, isso é os dígitos decimais da coluna na fonte de dados. Para tipos de dados de intervalo que contêm um componente de tempo, esta coluna contém o número de dígitos à direita da vírgula decimal (frações de segundo). Para tipos de dados de intervalo que não contêm um componente de tempo, essa coluna é 0. Para obter mais informações sobre como os dígitos decimais, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: Tipos de dados. NULL é retornado para os tipos de dados onde DECIMAL_DIGITS não é aplicável.|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|Para tipos de dados numéricos, 10 ou 2. Se ele for 10, os valores de COLUMN_SIZE e DECIMAL_DIGITS dar o número de dígitos decimais, permitido para a coluna. Por exemplo, uma coluna DECIMAL(12,5) retornaria um NUM_PREC_RADIX de 10, um COLUMN_SIZE de 12 e um DECIMAL_DIGITS 5; uma coluna FLOAT poderia retornar um NUM_PREC_RADIX de 10, um COLUMN_SIZE 15 e DECIMAL_DIGITS de NULL.<br /><br /> Se ele for 2, os valores de COLUMN_SIZE e DECIMAL_DIGITS dar o número de bits permitidos na coluna. Por exemplo, uma coluna FLOAT pode retornar uma base de 2, um COLUMN_SIZE de 53 e DECIMAL_DIGITS de NULL.<br /><br /> NULL é retornado para os tipos de dados onde NUM_PREC_RADIX não é aplicável.|  
|PERMITE VALOR NULO (ODBC 1.0)|11|Smallint não NULL|SQL_NO_NULLS se a coluna não pode incluir valores nulos.<br /><br /> SQL_NULLABLE se a coluna aceita valores nulos.<br /><br /> SQL_NULLABLE_UNKNOWN se não se sabe se a coluna aceita valores nulos.<br /><br /> O valor retornado para esta coluna é diferente do valor retornado para a coluna IS_NULLABLE. A coluna permite valor nula indica com certeza que uma coluna pode aceitar valores nulos, mas não é possível indicar, com certeza que uma coluna não aceita valores nulos. Indica a coluna IS_NULLABLE com certeza que uma coluna não pode aceitar valores nulos, mas não é possível indicar, com certeza que uma coluna aceita valores nulos.|  
|COMENTÁRIOS (ODBC 1.0)|12|Varchar|Uma descrição da coluna.|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|O valor padrão da coluna. O valor nessa coluna deve ser interpretado como uma cadeia de caracteres que ele seja colocado entre aspas.<br /><br /> Se NULL for especificado como o valor padrão, esta coluna é a palavra NULL, que não são colocada entre aspas. Se o valor padrão não pode ser representado sem truncamento, esta coluna contém truncados, sem colocar aspas simples. Se nenhum valor padrão tiver sido especificado, essa coluna é NULL.<br /><br /> O valor de COLUMN_DEF pode ser usado ao gerar uma nova definição de coluna, exceto quando ela contém o valor TRUNCADO.|  
|SQL_DATA_TYPE (ODBC 3.0)|14|Smallint não NULL|Tipo de dados SQL, como ele aparece no campo SQL_DESC_TYPE registro do IRD. Isso pode ser um tipo de dados SQL ODBC ou um tipo de dados SQL específica do driver. Esta coluna é igual à coluna DATA_TYPE, exceto para tipos de dados de data e hora e intervalo. Esta coluna retorna o tipo de dados nonconcise (como SQL_DATETIME ou SQL_INTERVAL), em vez do tipo de dados concisa (como SQL_TYPE_DATE ou SQL_INTERVAL_YEAR_TO_MONTH) para data e hora e tipos de dados de intervalo. Se esta coluna retorna SQL_DATETIME ou SQL_INTERVAL, o tipo de dados específico pode ser determinado da coluna SQL_DATETIME_SUB. Para obter uma lista dos tipos de dados SQL ODBC válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice d: Tipos de dados. Para obter informações sobre tipos de dados SQL específico do driver, consulte a documentação do driver.<br /><br /> Os tipos de dados retornados para o ODBC 3. *x* e o ODBC 2. *x* aplicativos podem ser diferentes. Para obter mais informações, consulte [compatibilidade com versões anteriores e em conformidade com padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|O código de subtipo para tipos de dados de data e hora e intervalo. Para outros tipos de dados, esta coluna retorna um valor nulo. Para obter mais informações sobre a data e hora e intervalo subcódigos, consulte "SQL_DESC_DATETIME_INTERVAL_CODE" na [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|Integer|O comprimento máximo em bytes de um caractere ou dados binários a coluna de tipo. Para todos os outros tipos de dados, esta coluna retorna um valor nulo.|  
|ORDINAL_POSITION (ODBC 3.0)|17|Integer não NULL|A posição ordinal da coluna na tabela. A primeira coluna na tabela é um número 1.|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|"Não" se a coluna não incluir valores nulos.<br /><br /> "Sim" se a coluna pode incluir valores nulos.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS em conformidade com ISO SQL não pode retornar uma cadeia de caracteres vazia.<br /><br /> O valor retornado para esta coluna é diferente do valor retornado para a coluna permite valor nula. (Consulte a descrição da coluna permite valor nula).|  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo declara buffers para o conjunto de resultados retornado por **SQLColumns**. Ele chama **SQLColumns** para retornar um conjunto de resultados que descreve cada coluna na tabela de funcionários. Em seguida, ele chama **SQLBindCol** para associar as colunas no conjunto de resultados para os buffers. Por fim, o aplicativo busca cada linha de dados com **SQLFetch** e processa-os.  
  
```  
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
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando os privilégios para uma coluna ou colunas|[Função SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscar várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Retornando colunas que identificam exclusivamente uma linha ou colunas atualizadas automaticamente por uma transação|[Função SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|Retornando estatísticas de tabela e índices|[Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Retornando uma lista de tabelas em uma fonte de dados|[Função SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
|Retornando os privilégios para uma tabela ou tabelas|[Função SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
