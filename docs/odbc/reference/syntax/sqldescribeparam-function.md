---
title: Função SQLDescribeParam | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 584e24e074a89670f0182fdfc29be1017b0a6ad6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqldescribeparam-function"></a>Função SQLDescribeParam
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLDescribeParam** retorna a descrição de um marcador de parâmetro associado com uma instrução SQL preparada. Essas informações também estão disponíveis nos campos de IPD.  
  
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
 [Entrada] Número de marcador de parâmetro ordenados consecutivamente em ordem crescente de parâmetro, começando em 1.  
  
 *DataTypePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o tipo de dados SQL do parâmetro. Esse valor é lido do campo de registro SQL_DESC_CONCISE_TYPE o IPD. Isso será um dos valores a [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) seção de apêndice d: os tipos de dados ou um tipo de dados SQL específico do driver.  
  
 Em ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP serão retornadas no  *\*DataTypePtr* para data, hora ou dados de carimbo de hora, respectivamente; no ODBC 2. *x*, SQL_DATE, SQL_TIME ou SQL_TIMESTAMP será retornado. O Gerenciador de Driver executa os mapeamentos necessários quando um ODBC 2. *x* aplicativo estiver trabalhando com um ODBC 3. *x* driver ou quando um ODBC 3. *x* aplicativo estiver trabalhando com um ODBC 2. *x* driver.  
  
 Quando *ColumnNumber* é igual a 0 (para uma coluna de indicador), SQL_BINARY é retornado no  *\*DataTypePtr* para indicadores de comprimento variável. (SQL_INTEGER é retornado se indicadores são usados por um ODBC 3. *x* aplicativo trabalhando com um ODBC 2. *x* driver ou por um ODBC 2. *x* aplicativo trabalhando com um ODBC 3. *x* driver.)  
  
 Para obter mais informações, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice d: os tipos de dados. Para obter informações sobre tipos de dados SQL específico do driver, consulte a documentação do driver.  
  
 *ParameterSizePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o tamanho, em caracteres, da coluna ou expressão do marcador de parâmetro correspondente conforme definido pela fonte de dados. Para obter mais informações sobre o tamanho da coluna, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *DecimalDigitsPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número de dígitos decimais da coluna ou expressão do parâmetro correspondente, conforme definido pela fonte de dados. Para obter mais informações sobre os dígitos decimais, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *NullablePtr*  
 [Saída] Ponteiro para um buffer no qual retornar um valor que indica se o parâmetro permite valores nulos. Esse valor é lido do campo SQL_DESC_NULLABLE o IPD. Um dos seguintes:  
  
-   SQL_NO_NULLS: O parâmetro não permite valores nulos (que é o valor padrão).  
  
-   SQL_NULLABLE: O parâmetro permite valores nulos.  
  
-   SQL_NULLABLE_UNKNOWN: O driver não pode determinar se o parâmetro permite valores nulos.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLDescribeParam** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDescribeParam** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice do descritor inválido|(DM) o valor especificado para o argumento *ParameterNumber* é menor que 1.<br /><br /> O valor especificado para o argumento *ParameterNumber* era maior que o número de parâmetros na instrução SQL associada.<br /><br /> O marcador de parâmetro fazia parte de uma instrução DML não.<br /><br /> O marcador de parâmetro fazia parte de um **selecione** lista.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|21S01|Lista de valores de inserção não corresponde a lista de colunas|O número de parâmetros no **inserir** instrução não coincidiu com o número de colunas na tabela chamada na instrução.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em uma aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM), a função foi chamada antes de chamar **SQLPrepare** ou **SQLExecDirect** para o *StatementHandle*.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLDescribeParam** função foi chamada.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Marcadores de parâmetro são numerados em ordem crescente de parâmetro, começando com 1, na ordem em que aparecem na instrução SQL.  
  
 **SQLDescribeParam** não retorna o tipo (entrada, entrada/saída ou saída) de um parâmetro em uma instrução SQL. Exceto em chamadas para procedimentos, todos os parâmetros em instruções SQL são parâmetros de entrada. Para determinar o tipo de cada parâmetro em uma chamada para um procedimento, um aplicativo chama **SQLProcedureColumns**.  
  
 Para obter mais informações, consulte [que descreve parâmetros](../../../odbc/reference/develop-app/describing-parameters.md).  
  
## <a name="code-example"></a>Exemplo de código  
 O exemplo a seguir solicita ao usuário uma instrução SQL e, em seguida, prepara essa instrução. Em seguida, ele chama **SQLNumParams** para determinar se a instrução contém todos os parâmetros. Se a instrução contiver parâmetros, ele chama **SQLDescribeParam** para descrever os parâmetros e **SQLBindParameter** para associá-los. Por fim, ele solicita ao usuário para os valores de quaisquer parâmetros e, em seguida, executa a instrução.  
  
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
|Executar uma instrução preparada do SQL|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparar uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
