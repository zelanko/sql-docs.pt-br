---
title: Função SQLDescribeParam | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c55668bb565bd383d170e7bf331630bf8b6adef1
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246595"
---
# <a name="sqldescribeparam-function"></a>Função SQLDescribeParam
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ODBC  
  
 **Resumo**  
 **SQLDescribeParam** retorna a descrição de um marcador de parâmetro associado a uma instrução SQL preparada. Essas informações também estão disponíveis nos campos do IPD.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLDescribeParam(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT *   DataTypePtr,  
      SQLULEN *       ParameterSizePtr,  
      SQLSMALLINT *   DecimalDigitsPtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *ParameterNumber*  
 Entrada Número do marcador de parâmetro Ordenado em sequência no aumento da ordem dos parâmetros, começando em 1.  
  
 *DataTypePtr*  
 Der Ponteiro para um buffer no qual retornar o tipo de dados SQL do parâmetro. Esse valor é lido no campo de registro de SQL_DESC_CONCISE_TYPE do IPD. Esse será um dos valores na seção tipos de [dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) do Apêndice D: tipos de dados ou um tipo de dados SQL específico do driver.  
  
 No ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME ou SQL_TYPE_TIMESTAMP serão retornados em * \* DataTypePtr* para dados de data, hora ou timestamp, respectivamente; no ODBC 2.* x*, SQL_DATE, SQL_TIME ou SQL_TIMESTAMP serão retornados. O Gerenciador de driver executa os mapeamentos necessários quando um ODBC 2. o aplicativo *x* está trabalhando com um ODBC 3. *x* driver ou quando um ODBC 3. o aplicativo *x* está funcionando com um ODBC 2. Driver *x* .  
  
 Quando *ColumnNumber* é igual a 0 (para uma coluna de indicador), SQL_BINARY é retornado em * \* DataTypePtr* para indicadores de comprimento variável. (SQL_INTEGER será retornado se os indicadores forem usados por um ODBC 3. *x* aplicativo trabalhando com um ODBC 2. Driver *x* ou por um ODBC 2. *x* aplicativo trabalhando com um ODBC 3. Driver *x* .)  
  
 Para obter mais informações, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice D: tipos de dados. Para obter informações sobre tipos de dados do SQL específicos do driver, consulte a documentação do driver.  
  
 *ParameterSizePtr*  
 Der Ponteiro para um buffer no qual retornar o tamanho, em caracteres, da coluna ou expressão do marcador de parâmetro correspondente, conforme definido pela fonte de dados. Para obter mais informações sobre o tamanho da coluna, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *DecimalDigitsPtr*  
 Der Ponteiro para um buffer no qual retornar o número de dígitos decimais da coluna ou expressão do parâmetro correspondente, conforme definido pela fonte de dados. Para obter mais informações sobre dígitos decimais, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *NullablePtr*  
 Der Ponteiro para um buffer no qual retornar um valor que indica se o parâmetro permite valores nulos. Esse valor é lido no campo SQL_DESC_NULLABLE do IPD. Um dos seguintes:  
  
-   SQL_NO_NULLS: o parâmetro não permite valores nulos (esse é o valor padrão).  
  
-   SQL_NULLABLE: o parâmetro permite valores nulos.  
  
-   SQL_NULLABLE_UNKNOWN: o driver não pode determinar se o parâmetro permite valores nulos.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLDescribeParam** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDescribeParam** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|(DM) o valor especificado para o argumento *ParameterNumber* é menor que 1.<br /><br /> O valor especificado para o argumento *ParameterNumber* era maior que o número de parâmetros na instrução SQL associada.<br /><br /> O marcador de parâmetro era parte de uma instrução não DML.<br /><br /> O marcador de parâmetro era parte de uma lista de **seleção** .|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|21S01|A lista de valores de inserção não corresponde à lista de colunas|O número de parâmetros na instrução **Insert** não correspondeu ao número de colunas na tabela nomeada na instrução.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) a função foi chamada antes de chamar **SQLPrepare** ou **SQLExecDirect** para o *StatementHandle*.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLDescribeParam** foi chamada.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Os marcadores de parâmetro são numerados em ordem crescente de parâmetros, começando com 1, na ordem em que aparecem na instrução SQL.  
  
 **SQLDescribeParam** não retorna o tipo (entrada, entrada/saída ou saída) de um parâmetro em uma instrução SQL. Exceto em chamadas para procedimentos, todos os parâmetros nas instruções SQL são parâmetros de entrada. Para determinar o tipo de cada parâmetro em uma chamada para um procedimento, um aplicativo chama **SQLProcedureColumns**.  
  
 Para obter mais informações, consulte [descrevendo parâmetros](../../../odbc/reference/develop-app/describing-parameters.md).  
  
## <a name="code-example"></a>Exemplo de código  
 O exemplo a seguir solicita ao usuário uma instrução SQL e, em seguida, prepara essa instrução. Em seguida, ele chama **SQLNumParams** para determinar se a instrução contém quaisquer parâmetros. Se a instrução contiver parâmetros, ele chamará **SQLDescribeParam** para descrever os parâmetros e **SQLBindParameter** para associá-los. Por fim, ele solicita ao usuário os valores de qualquer parâmetro e, em seguida, executa a instrução.  
  
```cpp  
SQLCHAR       Statement[100];  
SQLSMALLINT   NumParams, i, DataType, DecimalDigits, Nullable;  
SQLUINTEGER   ParamSize;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement and prepare it.  
GetSQLStatement(Statement);  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Check to see if there are any parameters. If so, process them.  
SQLNumParams(hstmt, &NumParams);  
if (NumParams) {  
   // Allocate memory for three arrays. The first holds pointers to buffers in which  
   // each parameter value will be stored in character form. The second contains the  
   // length of each buffer. The third contains the length/indicator value for each  
   // parameter.  
   SQLPOINTER * PtrArray = (SQLPOINTER *) malloc(NumParams * sizeof(SQLPOINTER));  
   SQLINTEGER * BufferLenArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
   SQLINTEGER * LenOrIndArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
  
   for (i = 0; i < NumParams; i++) {  
   // Describe the parameter.  
   SQLDescribeParam(hstmt, i + 1, &DataType, &ParamSize, &DecimalDigits, &Nullable);  
  
   // Call a helper function to allocate a buffer in which to store the parameter  
   // value in character form. The function determines the size of the buffer from  
   // the SQL data type and parameter size returned by SQLDescribeParam and returns  
   // a pointer to the buffer and the length of the buffer.  
   AllocParamBuffer(DataType, ParamSize, &PtrArray[i], &BufferLenArray[i]);  
  
   // Bind the memory to the parameter. Assume that we only have input parameters.  
   SQLBindParameter(hstmt, i + 1, SQL_PARAM_INPUT, SQL_C_CHAR, DataType, ParamSize,  
         DecimalDigits, PtrArray[i], BufferLenArray[i],  
         &LenOrIndArray[i]);  
  
   // Prompt the user for the value of the parameter and store it in the memory  
   // allocated earlier. For simplicity, this function does not check the value  
   // against the information returned by SQLDescribeParam. Instead, the driver does  
   // this when the statement is executed.  
   GetParamValue(PtrArray[i], BufferLenArray[i], &LenOrIndArray[i]);  
   }  
}  
  
// Execute the statement.  
SQLExecute(hstmt);  
  
// Process the statement further, such as retrieving results (if any) and closing the  
// cursor (if any). Code not shown.  
  
// Free the memory allocated for each parameter and the memory allocated for the arrays  
// of pointers, buffer lengths, and length/indicator values.  
for (i = 0; i < NumParams; i++) free(PtrArray[i]);  
free(PtrArray);  
free(BufferLenArray);  
free(LenOrIndArray);  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparando uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
