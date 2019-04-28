---
title: Função SQLDescribeParam | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62d61d43638c0ca6e3e43da83367dff461033463
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62982300"
---
# <a name="sqldescribeparam-function"></a>Função SQLDescribeParam
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLDescribeParam** retorna a descrição de um marcador de parâmetro associado com uma instrução SQL preparada. Essas informações também estão disponíveis nos campos do IPD.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLDescribeParam(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT *   DataTypePtr,  
      SQLULEN *       ParameterSizePtr,  
      SQLSMALLINT *   DecimalDigitsPtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="argument"></a>Argumento  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *ParameterNumber*  
 [Entrada] Número do marcador de parâmetro ordenado em sequência em ordem crescente de parâmetro, começando em 1.  
  
 *DataTypePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o tipo de dados SQL do parâmetro. Esse valor é lido do campo SQL_DESC_CONCISE_TYPE registro do IPD. Esse será um dos valores de [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) seção de apêndice d: Tipos de dados, ou um tipo de dados SQL específica do driver.  
  
 Em ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP será retornado  *\*DataTypePtr* para data, hora ou dados de carimbo de hora, respectivamente; no ODBC 2. *x*, SQL_DATE, SQL_TIME ou SQL_TIMESTAMP serão retornados. O Gerenciador de Driver executa os mapeamentos necessários quando um ODBC 2. *x* aplicativo está funcionando com um ODBC 3. *x* driver ou quando um ODBC 3. *x* aplicativo está funcionando com um ODBC 2. *x* driver.  
  
 Quando *ColumnNumber* é igual a 0 (para uma coluna de indicador), SQL_BINARY é retornado na  *\*DataTypePtr* para indicadores de comprimento variável. (SQL_INTEGER é retornada se os indicadores são usados por um ODBC 3. *x* aplicativo trabalhar com um ODBC 2. *x* driver ou por um ODBC 2. *x* aplicativo trabalhar com um ODBC 3. *x* driver.)  
  
 Para obter mais informações, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice d: Tipos de dados. Para obter informações sobre tipos de dados SQL específico do driver, consulte a documentação do driver.  
  
 *ParameterSizePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o tamanho, em caracteres, da coluna ou expressão do marcador de parâmetro correspondente, conforme definido pela fonte de dados. Para obter mais informações sobre o tamanho da coluna, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *DecimalDigitsPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número de dígitos decimais da coluna ou expressão do parâmetro correspondente, conforme definido pela fonte de dados. Para obter mais informações sobre como os dígitos decimais, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *NullablePtr*  
 [Saída] Ponteiro para um buffer no qual retornar um valor que indica se o parâmetro permite valores nulos. Esse valor é lido do campo SQL_DESC_NULLABLE do IPD. Um dos seguintes:  
  
-   SQL_NO_NULLS: O parâmetro não permite valores nulos (que é o valor padrão).  
  
-   SQL_NULLABLE: O parâmetro permite valores nulos.  
  
-   SQL_NULLABLE_UNKNOWN: O driver não pode determinar se o parâmetro permite valores nulos.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLDescribeParam** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDescribeParam** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|(DM) o valor especificado para o argumento *ParameterNumber* for menor que 1.<br /><br /> O valor especificado para o argumento *ParameterNumber* era maior que o número de parâmetros na instrução SQL associada.<br /><br /> O marcador de parâmetro fazia parte de uma instrução DML não.<br /><br /> O marcador de parâmetro fazia parte de um **selecionar** lista.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|21S01|Lista de valores de inserção não corresponde a lista de colunas|O número de parâmetros na **inserir** instrução não correspondeu ao número de colunas na tabela chamada na instrução.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM), a função foi chamada antes de chamar **SQLPrepare** ou **SQLExecDirect** para o *StatementHandle*.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLDescribeParam** função foi chamada.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Marcadores de parâmetro são numerados em ordem crescente de parâmetro, começando com 1, na ordem em que eles aparecem na instrução SQL.  
  
 **SQLDescribeParam** não retorna o tipo (entrada, entrada/saída ou de saída) de um parâmetro em uma instrução SQL. Exceto em chamadas para procedimentos, todos os parâmetros em instruções SQL são parâmetros de entrada. Para determinar o tipo de cada parâmetro em uma chamada para um procedimento, um aplicativo chama **SQLProcedureColumns**.  
  
 Para obter mais informações, consulte [descrevendo parâmetros](../../../odbc/reference/develop-app/describing-parameters.md).  
  
## <a name="code-example"></a>Exemplo de código  
 O exemplo a seguir solicita ao usuário para uma instrução SQL e, em seguida, prepara essa instrução. Em seguida, ele chama **SQLNumParams** para determinar se a instrução contém todos os parâmetros. Se a instrução contiver parâmetros, ele chama **SQLDescribeParam** para descrever os parâmetros e **SQLBindParameter** vinculá-las. Por fim, ele solicita ao usuário para os valores de quaisquer parâmetros e, em seguida, executa a instrução.  
  
```  
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
|Um buffer de associação a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executar uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Como preparar uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
