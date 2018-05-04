---
title: Função SQLBindParameter | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLBindParameter
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6dabf41f117227830cdf536f4d17f32b71a2d09
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlbindparameter-function"></a>Função SQLBindParameter
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 2.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLBindParameter** associa um buffer para um marcador de parâmetro em uma instrução SQL. **SQLBindParameter** dá suporte à associação a um tipo de dados Unicode C, mesmo que o driver subjacente não oferece suporte a dados Unicode.  
  
> [!NOTE]  
>  Esta função substitui a função ODBC 1.0 **SQLSetParam**. Para obter mais informações, consulte "Comentários".  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLBindParameter(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT     InputOutputType,  
      SQLSMALLINT     ValueType,  
      SQLSMALLINT     ParameterType,  
      SQLULEN         ColumnSize,  
      SQLSMALLINT     DecimalDigits,  
      SQLPOINTER      ParameterValuePtr,  
      SQLLEN          BufferLength,  
      SQLLEN *        StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *ParameterNumber*  
 [Entrada] Número de parâmetro, ordenados consecutivamente em ordem crescente de parâmetro, começando em 1.  
  
 *InputOutputType*  
 [Entrada] O tipo do parâmetro. Para obter mais informações, consulte "*InputOutputType* argumento" em "Comentários".  
  
 *ValueType*  
 [Entrada] O tipo de dados C do parâmetro. Para obter mais informações, consulte "*ValueType* argumento" em "Comentários".  
  
 *ParameterType*  
 [Entrada] O tipo de dados SQL do parâmetro. Para obter mais informações, consulte "*ParameterType* argumento" em "Comentários".  
  
 *ColumnSize*  
 [Entrada] O tamanho da coluna ou expressão do marcador de parâmetro correspondente. Para obter mais informações, consulte "*ColumnSize* argumento" em "Comentários".  
  
 Se o aplicativo será executado em um sistema de operacional do Windows de 64 bits, consulte [informações de ODBC de 64 bits](../../../odbc/reference/odbc-64-bit-information.md).  
  
 *DecimalDigits*  
 [Entrada] Os dígitos decimais da coluna ou expressão do marcador de parâmetro correspondente. Para obter mais informações sobre o tamanho da coluna, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *ParameterValuePtr*  
 [Entrada adiada] Um ponteiro para um buffer de dados do parâmetro. Para obter mais informações, consulte "*ParameterValuePtr* argumento" em "Comentários".  
  
 *BufferLength*  
 [Entrada/saída] Comprimento do *ParameterValuePtr* buffer em bytes. Para obter mais informações, consulte "*BufferLength* argumento" em "Comentários".  
  
 Consulte [informações de ODBC de 64 bits](../../../odbc/reference/odbc-64-bit-information.md), se o aplicativo será executado em um sistema operacional de 64 bits.  
  
 *StrLen_or_IndPtr*  
 [Entrada adiada] Um ponteiro para um buffer para o comprimento do parâmetro. Para obter mais informações, consulte "*StrLen_or_IndPtr* argumento" em "Comentários".  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLBindParameter** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLBindParameter** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|O tipo de dados identificado pelo *ValueType* argumento não pode ser convertido para o tipo de dados identificado pelo *ParameterType* argumento. Observe que esse erro pode ser retornado por **SQLExecDirect**, **SQLExecute**, ou **SQLPutData** em tempo de execução, em vez de por **SQLBindParameter**.|  
|07009|Índice do descritor inválido|(DM) o valor especificado para o argumento *ParameterNumber* foi menor que 1.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no **MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY003|Tipo de buffer de aplicativo inválido|O valor especificado pelo argumento *ValueType* não era um tipo de dados válido do C ou SQL_C_DEFAULT.|  
|HY004|Tipo de dados SQL inválido|O valor especificado para o argumento *ParameterType* não era um identificador de tipo de dados SQL ODBC válido nem um identificador de tipo de dados do específicos do driver SQL com suporte pelo driver.|  
|HY009|Valor de argumento inválido|(DM) o argumento *ParameterValuePtr* foi um ponteiro nulo, o argumento *StrLen_or_IndPtr* era um ponteiro nulo e o argumento *InputOutputType* não era SQL_PARAM_ SAÍDA.<br /><br /> SQL_PARAM_OUTPUT (DM), em que o argumento *ParameterValuePtr* foi um ponteiro nulo, o tipo C foi char ou binary e o BufferLength (*cbValueMax*) foi maior que 0.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando **SQLBindParameter** foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY021|Informações do descritor inconsistentes|As informações de descritor verificadas durante uma verificação de consistência não estavam consistentes. (Consulte a seção "Verificações de consistência" **SQLSetDescField**.)<br /><br /> O valor especificado para o argumento *DecimalDigits* estava fora do intervalo de valores com suporte pela fonte de dados para uma coluna do tipo de dados SQL especificado pelo *ParameterType* argumento.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor em *BufferLength* era menor do que 0. (Consulte a descrição do campo SQL_DESC_DATA_PTR em **SQLSetDescField**.)|  
|HY104|Valor de precisão ou escala inválido|O valor especificado para o argumento *ColumnSize* ou *DecimalDigits* estava fora do intervalo de valores com suporte pela fonte de dados para uma coluna do tipo de dados SQL especificado pelo  *ParameterType* argumento.|  
|HY105|Tipo de parâmetro inválido|(DM) o valor especificado para o argumento *InputOutputType* era inválido. (Consulte "Comentários".)|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A driver ou fonte de dados não suporta a conversão especificada pela combinação do valor especificado para o argumento *ValueType* e o valor específico do driver especificado para o argumento *ParameterType*.<br /><br /> O valor especificado para o argumento *ParameterType* era um identificador de tipo de dados ODBC SQL válido para a versão do ODBC com suporte pelo driver, mas não era compatível com a driver ou fonte de dados.<br /><br /> O driver suporta apenas o ODBC 2. *x* e o argumento *ValueType* foi um dos seguintes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e todos os tipos de dados de intervalo C listados na [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) no Apêndice d: os tipos de dados.<br /><br /> O driver só dá suporte a versões ODBC anteriores 3.50 e o argumento *ValueType* foi SQL_C_GUID.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo chama **SQLBindParameter** para associar cada marcador de parâmetro em uma instrução SQL. Associações permanecem em vigor até que o aplicativo chama **SQLBindParameter** novamente, chama **SQLFreeStmt** com a opção SQL_RESET_PARAMS ou chamadas **SQLSetDescField** para Defina o campo de cabeçalho SQL_DESC_COUNT de APD como 0.  
  
 Para obter mais informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md). Para obter mais informações sobre tipos de dados de parâmetro e marcadores de parâmetro, consulte [tipos de dados do parâmetro](../../../odbc/reference/appendixes/parameter-data-types.md) e [marcadores de parâmetro](../../../odbc/reference/appendixes/parameter-markers.md) na gramática do apêndice c: SQL.  
  
## <a name="parameternumber-argument"></a>Argumento ParameterNumber  
 Se *ParameterNumber* na chamada para **SQLBindParameter** é maior que o valor de SQL_DESC_COUNT, **SQLSetDescField** é chamado para aumentar o valor de SQL_DESC_ Contagem de *ParameterNumber*.  
  
## <a name="inputoutputtype-argument"></a>Argumento InputOutputType  
 O *InputOutputType* argumento especifica o tipo do parâmetro. Esse argumento define o campo SQL_DESC_PARAMETER_TYPE o IPD. Todos os parâmetros em instruções SQL que não chamam procedimentos, como **inserir** , as instruções são *entrada * * parâmetros*. Parâmetros em chamadas de procedimento podem ser de entrada, entradam/saídam ou parâmetros de saída. (Um aplicativo chama **SQLProcedureColumns** para determinar o tipo de um parâmetro em uma chamada de procedimento; parâmetros cujo tipo não pode ser determinado são considerados parâmetros de entrada.)  
  
 O *InputOutputType* argumento for um dos seguintes valores:  
  
-   SQL_PARAM_INPUT. O parâmetro de marca um parâmetro em uma instrução SQL que não chama um procedimento, como um **inserir** instrução ou marca um parâmetro de entrada em um procedimento. Por exemplo, os parâmetros no **INSERT INTO funcionário VALUES (?,?,?)**  são parâmetros de entrada, enquanto os parâmetros no **{chamar AddEmp (?,?,?)}**  pode ser, mas não são necessariamente, parâmetros de entrada.  
  
     Quando a instrução é executada, o driver envia dados para o parâmetro para a fonte de dados; o \* *ParameterValuePtr* buffer deve conter um valor válido de entrada, ou o **StrLen_or_IndPtr* buffer deve conter SQL_NULL_DATA, SQL_DATA_AT_EXEC ou o resultado da SQL_LEN_DATA_AT Macro EXEC.  
  
     Se um aplicativo não é possível determinar o tipo de um parâmetro em uma chamada de procedimento, ele define *InputOutputType* para SQL_PARAM_INPUT; se a fonte de dados retorna um valor para o parâmetro, o driver descartará-lo.  
  
-   SQL_PARAM_INPUT_OUTPUT. O parâmetro de marca um parâmetro de entrada/saída em um procedimento. Por exemplo, o parâmetro no **{chamar GetEmpDept(?)}**  é um parâmetro de entrada e saída que aceita o nome de um funcionário e retorna o nome do departamento do funcionário.  
  
     Quando a instrução é executada, o driver envia dados para o parâmetro para a fonte de dados; o \* *ParameterValuePtr* buffer deve conter um valor válido de entrada, ou o \* *StrLen_or_IndPtr* buffer deve conter SQL_NULL_DATA, SQL_DATA_AT_EXEC ou o resultado de a macro SQL_LEN_DATA_AT_EXEC. Depois que a instrução é executada, o driver retorna dados para o parâmetro do aplicativo. Se a fonte de dados não retornar um valor para um parâmetro de entrada/saída, o driver define o **StrLen_or_IndPtr* buffer como SQL_NULL_DATA.  
  
    > [!NOTE]  
    >  Quando um aplicativo ODBC 1.0 chama **SQLSetParam** em um driver de ODBC 2.0, o Gerenciador de Driver converte isso para uma chamada para **SQLBindParameter** no qual o *InputOutputType* argumento é definido como SQL_PARAM_INPUT_OUTPUT.  
  
-   SQL_PARAM_OUTPUT. O parâmetro de marca o valor de retorno de um procedimento ou um parâmetro de saída em um procedimento; em ambos os casos, eles são conhecidos como *parâmetros de saída*. Por exemplo, o parâmetro no **{? = chamar GetNextEmpID}** é um parâmetro de saída que retorna a próxima ID de funcionário.  
  
     Depois que a instrução é executada, o driver retorna dados para o parâmetro para o aplicativo, a menos que o *ParameterValuePtr* e *StrLen_or_IndPtr* argumentos são ambos os ponteiros nulos, caso em que o driver descartará o valor de saída. Se a fonte de dados não retornar um valor para um parâmetro de saída, o driver define o **StrLen_or_IndPtr* buffer como SQL_NULL_DATA.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. Indica que um parâmetro de entrada/saída deve ser transmitido. **SQLGetData** pode ler os valores de parâmetro em partes. *BufferLength* foi ignorada porque o tamanho do buffer será determinado na chamada de **SQLGetData**. O valor de *StrLen_or_IndPtr* buffer deve conter SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC. Um parâmetro deve ser associado como um parâmetro de dados em execução (Disk) na entrada se ela será transmitida na saída. *ParameterValuePtr* pode ser qualquer valor de ponteiro null não será retornado por **SQLParamData** conforme definido pelo usuário cujo valor do token foi passado com *ParameterValuePtr* para entrada e saída. Para obter mais informações, consulte [recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_PARAM_OUTPUT_STREAM. Mesmo que SQL_PARAM_INPUT_OUTPUT_STREAM, para um parâmetro de saída. **StrLen_or_IndPtr* é ignorado na entrada.  
  
 A tabela a seguir lista as combinações diferentes de *InputOutputType* e **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|Resultado|Marcar em ParameterValuePtr|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*len*) ou SQL_DATA_AT_EXEC|Entrada em partes|*ParameterValuePtr* pode ser qualquer valor de ponteiro que será retornado por **SQLParamData** conforme definido pelo usuário cujo valor do token foi passado com *ParameterValuePtr*.|  
|SQL_PARAM_INPUT|Não SQL_LEN_DATA_AT_EXEC (*len*) ou SQL_DATA_AT_EXEC|Buffer de associar a entrada|*ParameterValuePtr* é o endereço do buffer de entrada.|  
|SQL_PARAM_OUTPUT|Ignorado na entrada.|Buffer de saída de associado|*ParameterValuePtr* é o endereço do buffer de saída.|  
|SQL_PARAM_OUTPUT_STREAM|Ignorado na entrada.|Fluxo de saída|*ParameterValuePtr* pode ser qualquer valor de ponteiro, que será retornado por **SQLParamData** conforme definido pelo usuário cujo valor do token foi passado com *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*len*) ou SQL_DATA_AT_EXEC|Entrada em partes e o buffer de saída de associado|*ParameterValuePtr* é o endereço do buffer de saída, também será retornado por **SQLParamData** conforme definido pelo usuário cujo valor do token foi passado com *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|Não SQL_LEN_DATA_AT_EXEC (*len*) ou SQL_DATA_AT_EXEC|Entrada buffer vinculado e o buffer de saída de associado|*ParameterValuePtr* é o endereço do buffer de entrada/saída compartilhado.|  
L_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*len*) ou SQL_DATA_AT_EXEC|Entrada em partes e fluxo de saída|*ParameterValuePtr* pode ser qualquer valor de ponteiro não nulo, que será retornado por **SQLParamData** conforme definido pelo usuário cujo valor do token foi passado com *ParameterValuePtr* de entrada e a saída.|  
  
> [!NOTE]  
>  O driver deve decidir quais tipos SQL são permitidos quando um aplicativo associar uma saída ou um parâmetro de entrada e saída, conforme transmitido. O Gerenciador de driver não irá gerar um erro para um tipo SQL inválido.  
  
## <a name="valuetype-argument"></a>Argumento de ValueType  
 O *ValueType* argumento especifica o tipo de dados C do parâmetro. Esse argumento define os campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE de APD. Isso deve ser um dos valores a [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) seção apêndice d: de tipos de dados.  
  
 Se o *ValueType* argumento é um dos tipos de dados de intervalo, o campo SQL_DESC_TYPE do *ParameterNumber* registro de APD é definido como SQL_INTERVAL, o campo SQL_DESC_CONCISE_TYPE de APD é definido como o tipo de dados de um intervalo e o campo SQL_DESC_DATETIME_INTERVAL_CODE do *ParameterNumber* registro é definido como um subcódigo para o tipo de dados de intervalo específico. (Consulte [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md).) O intervalo padrão à esquerda (2) de precisão e a precisão de segundos de intervalo padrão (6), conforme definido nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION de APD, respectivamente, são usadas para os dados. Se a precisão padrão não for apropriado, o aplicativo deve definir explicitamente o campo do descritor por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Se o *ValueType* argumento é um dos tipos de dados de data e hora, o campo SQL_DESC_TYPE do *ParameterNumber* registro de APD é definido como SQL_DATETIME, o campo SQL_DESC_CONCISE_TYPE da *ParameterNumber* registro de APD é definido como o tipo de dados datetime concisa C e o campo SQL_DESC_DATETIME_INTERVAL_CODE do *ParameterNumber* registro é definido como um subcódigo para a data e hora específica tipo de dados. (Consulte [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Se o *ValueType* argumento é um tipo de dados SQL_C_NUMERIC, a precisão padrão (que é definido pelo driver) e a escala padrão (0), conforme definido nos campos SQL_DESC_PRECISION e SQL_DESC_SCALE de APD, são usadas para os dados. Se a escala ou precisão padrão não for apropriada, o aplicativo deve definir explicitamente o campo do descritor por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 SQL_C_DEFAULT Especifica que o valor do parâmetro ser transferida do tipo de dados padrão C para o tipo de dados SQL especificado com *ParameterType*.  
  
 Você também pode especificar um tipo de dados estendido C. Para obter mais informações, consulte [tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 Para obter mais informações, consulte [tipos de dados C padrão](../../../odbc/reference/appendixes/default-c-data-types.md), [converter dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md), e [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no Apêndice d: os tipos de dados.  
  
## <a name="parametertype-argument"></a>Argumento ParameterType  
 Isso deve ser um dos valores listados no [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) seção de apêndice d: os tipos de dados, ou deve ser um valor específico de driver. Esse argumento define os campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE do IPD.  
  
 Se o *ParameterType* argumento é um dos identificadores de datetime, o campo SQL_DESC_TYPE do IPD é definido como SQL_DATETIME, o campo SQL_DESC_CONCISE_TYPE do IPD está definido para o tipo de dados datetime concisa SQL e o SQL_DESC_ Campo DATETIME_INTERVAL_CODE é definido como o valor de subcódigo datetime apropriado.  
  
 Se *ParameterType* é um dos identificadores de intervalo, o campo SQL_DESC_TYPE do IPD é definido como SQL_INTERVAL, o campo SQL_DESC_CONCISE_TYPE do IPD está definido para o tipo de dados de intervalo SQL conciso e o SQL_DESC_DATETIME_ Campo INTERVAL_CODE do IPD é definido como o subcódigo de intervalo apropriado. O campo SQL_DESC_DATETIME_INTERVAL_PRECISION do IPD está definido para a precisão à esquerda do intervalo, e o campo SQL_DESC_PRECISION é definido como a precisão de segundos de intervalo, se aplicável. Se o valor padrão de SQL_DESC_DATETIME_INTERVAL_PRECISION ou SQL_DESC_PRECISION não é apropriado, o aplicativo deve definir explicitamente-lo chamando **SQLSetDescField**. Para obter mais informações sobre qualquer um desses campos, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Se o *ValueType* argumento é um tipo de dados SQL_NUMERIC a precisão padrão (que é definido pelo driver) e a escala padrão (0), conforme definido nos campos de IPD, SQL_DESC_PRECISION e SQL_DESC_SCALE são usados para os dados. Se a escala ou precisão padrão não for apropriada, o aplicativo deve definir explicitamente o campo do descritor por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Para obter informações sobre como os dados são convertidos, consulte [converter dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) e [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no Apêndice d: os tipos de dados.  
  
## <a name="columnsize-argument"></a>Argumento ColumnSize  
 O *ColumnSize* argumento especifica o tamanho da coluna ou expressão que corresponde ao marcador de parâmetro, o comprimento de dados, ou ambos. Esse argumento define diferentes campos de IPD, dependendo do tipo de dados SQL (o *ParameterType* argumento). As seguintes regras se aplicam a este mapeamento:  
  
-   Se *ParameterType* é SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY ou um dos concisa SQL datetime ou intervalo de tipos de dados, o campo SQL_DESC_LENGTH do IPD for definido como o valor de  *ColumnSize*. (Para obter mais informações, consulte o [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) seção apêndice d: os tipos de dados.)  
  
-   Se *ParameterType* é SQL_DECIMAL, SQL_NUMERIC, SQL_FLOAT, SQL_REAL ou SQL_DOUBLE, o campo SQL_DESC_PRECISION do IPD é definido como o valor de *ColumnSize*.  
  
-   Para outros tipos de dados, o *ColumnSize* argumento será ignorado.  
  
 Para obter mais informações, consulte "Passando valores de parâmetro" e SQL_DATA_AT_EXEC em "*StrLen_or_IndPtr* argumento."  
  
## <a name="decimaldigits-argument"></a>Argumento DecimalDigits  
 Se *ParameterType* é SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND ou SQL_INTERVAL_MINUTE_TO_SECOND, o campo SQL_DESC_PRECISION do IPD está definido para *DecimalDigits*. Se *ParameterType* é SQL_NUMERIC ou SQL_DECIMAL, o campo SQL_DESC_SCALE do IPD é definido como *DecimalDigits*. Para todos os outros tipos de dados, o *DecimalDigits* argumento será ignorado.  
  
## <a name="parametervalueptr-argument"></a>Argumento ParameterValuePtr  
 O *ParameterValuePtr* argumento aponta para um buffer que, quando **SQLExecute** ou **SQLExecDirect** é chamado, que contém os dados reais para o parâmetro. Os dados devem estar no formato especificado pelo *ValueType* argumento. Esse argumento define o campo SQL_DESC_DATA_PTR APD. Um aplicativo pode definir o *ParameterValuePtr* argumento para um ponteiro nulo, contanto que  *\*StrLen_or_IndPtr* é SQL_NULL_DATA ou SQL_DATA_AT_EXEC. (Isso se aplica apenas a entrada ou entrada/saída parâmetros.)  
  
 Se \* *StrLen_or_IndPtr* é o resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro ou SQL_DATA_AT_EXEC, em seguida, *ParameterValuePtr* é um valor de ponteiro definido pelo aplicativo que está associado com o parâmetro. Ele é retornado para o aplicativo por meio de **SQLParamData**. Por exemplo, *ParameterValuePtr* pode ser um token diferente de zero, como um número de parâmetro, um ponteiro para dados ou um ponteiro para uma estrutura que o aplicativo usado para associar parâmetros de entrada. No entanto, observe que, se o parâmetro é um parâmetro de entrada/saída, *ParameterValuePtr* deve ser um ponteiro para um buffer em que o valor de saída será armazenado. Se o valor do atributo de instrução SQL_ATTR_PARAMSET_SIZE for maior que 1, o aplicativo pode usar o valor apontado pelo atributo da instrução SQL_ATTR_PARAMS_PROCESSED_PTR junto com o *ParameterValuePtr* argumento. Por exemplo, *ParameterValuePtr* pode apontar para uma matriz de valores e o aplicativo pode usar o valor apontado por SQL_ATTR_PARAMS_PROCESSED_PTR para recuperar o valor correto da matriz. Para obter mais informações, consulte "Passando valores de parâmetro" nesta seção.  
  
 Se o *InputOutputType* argumento é SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT, *ParameterValuePtr* aponta para um buffer no qual o driver retorna o valor de saída. Se o procedimento retorna um ou mais conjuntos de resultados, o \* *ParameterValuePtr* buffer não é garantido para ser definida até que todas as contagens de linha/conjuntos de resultados foram processadas. Se o buffer não é definido até que o processamento é concluído, os parâmetros de saída e valores de retorno não estarão disponíveis até **SQLMoreResults** retorna SQL_NO_DATA. Chamando **SQLCloseCursor** ou **SQLFreeStmt** com uma opção de SQL_CLOSE fará com que esses valores sejam descartadas.  
  
 Se o valor do atributo de instrução SQL_ATTR_PARAMSET_SIZE for maior que 1, *ParameterValuePtr* aponta para uma matriz. Uma única instrução SQL processa o conjunto completo de valores de entrada para um parâmetro de entrada ou entrada/saída e retorna uma matriz de valores de saída para uma entrada/saída ou parâmetro de saída.  
  
## <a name="bufferlength-argument"></a>Argumento BufferLength  
 Para dados de caracteres e binários C, o *BufferLength* argumento especifica o comprimento do \* *ParameterValuePtr* buffer (se for um único elemento) ou o comprimento de um elemento de \* *ParameterValuePtr* de matriz (se o valor do atributo de instrução SQL_ATTR_PARAMSET_SIZE é maior que 1). Esse argumento define o campo de registro SQL_DESC_OCTET_LENGTH APD. Se o aplicativo especificar vários valores, *BufferLength* é usado para determinar a localização dos valores a **ParameterValuePtr* de matriz, na entrada e na saída. Para parâmetros de entrada/saída e saída, ele é usado para determinar se deseja truncar os dados de caracteres e binários C na saída:  
  
-   Para dados de caractere C, se o número de bytes disponíveis para retornar é maior que ou igual a *BufferLength*, os dados em \* *ParameterValuePtr* será truncado para  *BufferLength* menos o comprimento de um caractere null de terminação e é terminada em nulo pelo driver.  
  
-   Para dados binários de C, se o número de bytes disponíveis para retornar for maior que *BufferLength*, os dados em \* *ParameterValuePtr* será truncado para *BufferLength*bytes.  
  
 Todos os outros tipos de dados C, o *BufferLength* argumento será ignorado. O comprimento do \* *ParameterValuePtr* buffer (se for um único elemento) ou o comprimento de um elemento no \* *ParameterValuePtr* (se o aplicativo chama dematriz **SQLSetStmtAttr** com um *atributo* argumento de SQL_ATTR_PARAMSET_SIZE para especificar vários valores para cada parâmetro) é assumido como o comprimento do tipo de dados C.  
  
 Para o fluxo de saída ou parâmetros de entrada/saída em fluxo, o *BufferLength* argumento é ignorado porque o tamanho do buffer é especificado em **SQLGetData**.  
  
> [!NOTE]  
>  Quando um aplicativo ODBC 1.0 chama **SQLSetParam** em um ODBC 3. *x* driver, o Gerenciador de Driver converterá isso em uma chamada para **SQLBindParameter** no qual o *BufferLength* argumento é sempre SQL_SETPARAM_VALUE_MAX. Porque o Gerenciador de Driver retornará um erro se um ODBC 3. *x* aplicativo define *BufferLength* para SQL_SETPARAM_VALUE_MAX, um ODBC 3. *x* driver pode usar isso para determinar quando ele é chamado por um aplicativo ODBC 1.0.  
  
> [!NOTE]  
>  Em **SQLSetParam**, a maneira na qual um aplicativo especifica o comprimento do **ParameterValuePtr* buffer para que o driver pode retornar caracteres ou dados binários e o modo no qual um aplicativo envia um matriz de caracteres ou valores de parâmetro binária para o driver, são definidos pelo driver.  
  
## <a name="strlenorindptr-argument"></a>Argumento StrLen_or_IndPtr  
 O *StrLen_or_IndPtr* argumento aponta para um buffer que, quando **SQLExecute** ou **SQLExecDirect** é chamado, contém um dos seguintes. (Este argumento define os campos de registro SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR dos ponteiros de parâmetro de aplicativo).  
  
-   O comprimento do valor do parâmetro armazenado em **ParameterValuePtr*. Isso é ignorado, exceto caracteres ou dados binários de C.  
  
-   SQL_NTS. O valor do parâmetro é uma cadeia de caracteres terminada em nulo.  
  
-   SQL_NULL_DATA. O valor do parâmetro é NULL.  
  
-   SQL_DEFAULT_PARAM. Um procedimento é usar o valor padrão de um parâmetro, em vez de um valor recuperado do aplicativo. Esse valor é válido somente em um procedimento chamado na sintaxe do ODBC canônico e somente se o *InputOutputType* é SQL_PARAM_INPUT, SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_INPUT_OUTPUT_STREAM. Quando \* *StrLen_or_IndPtr* é SQL_DEFAULT_PARAM, o *ValueType*, *ParameterType*, *ColumnSize*,  *DecimalDigits*, *BufferLength*, e *ParameterValuePtr* argumentos para parâmetros de entrada são ignorados e são usados apenas para definir o valor do parâmetro de saída para a entrada / parâmetros de saída.  
  
-   O resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro. Os dados para o parâmetro serão enviados com **SQLPutData**. Se o *ParameterType* argumento é SQL_LONGVARBINARY, SQL_LONGVARCHAR ou uma longa, tipo de dados de específico de fonte de dados, e o driver retorna "Y" para o tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo**, *comprimento* é o número de bytes de dados a serem enviados para o parâmetro; caso contrário, *comprimento* deve ser um valor não negativo e será ignorado. Para obter mais informações, consulte "Passando valores de parâmetro," nesta seção.  
  
     Por exemplo, para especificar que 10.000 bytes de dados serão enviados com **SQLPutData** em uma ou mais chamadas para um parâmetro SQL_LONGVARCHAR, define um aplicativo **StrLen_or_IndPtr* como SQL_LEN_DATA_AT_EXEC ( 10000).  
  
-   SQL_DATA_AT_EXEC. Os dados para o parâmetro serão enviados com **SQLPutData**. Esse valor é usado por aplicativos ODBC 1.0 quando eles chamam ODBC 3. *x* drivers. Para obter mais informações, consulte "Passando valores de parâmetro," nesta seção.  
  
 Se *StrLen_or_IndPtr* é um ponteiro nulo, o driver pressupõe que todos os valores de parâmetro de entrada não forem nulos e que os dados binários e de caractere são terminada em nulo. Se *InputOutputType* é SQL_PARAM_OUTPUT ou SQL_PARAM_OUTPUT_STREAM e *ParameterValuePtr* e *StrLen_or_IndPtr* são ambos os ponteiros nulos, descarta o driver o valor de saída.  
  
> [!NOTE]  
>  Os desenvolvedores de aplicativos são altamente desaconselhável da especificação de um ponteiro nulo para *StrLen_or_IndPtr* quando o tipo de dados do parâmetro é SQL_C_BINARY. Para certificar-se de que um driver inesperadamente não truncar dados SQL_C_BINARY, *StrLen_or_IndPtr* deve conter um ponteiro para um valor de comprimento válido.  
  
 Se o *InputOutputType* é SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM ou SQL_PARAM_OUTPUT_STREAM, *StrLen_or_IndPtr* aponta para um buffer no qual o driver retorna SQL_NULL_DATA, o número de bytes disponíveis para retornar em \* *ParameterValuePtr* (excluindo o byte nulo de terminação de dados de caracteres), ou SQL_NO_TOTAL (se o número de bytes disponíveis retorno não pode ser determinado). Se o procedimento retorna um ou mais conjuntos de resultados, o **StrLen_or_IndPtr* buffer não é garantido para ser definida até que todos os resultados foram buscados.  
  
 Se o valor do atributo de instrução SQL_ATTR_PARAMSET_SIZE for maior que 1, *StrLen_or_IndPtr* aponta para uma matriz de valores SQLLEN. Eles podem ser qualquer um dos valores listados anteriormente nesta seção e são processados com uma única instrução SQL.  
  
## <a name="passing-parameter-values"></a>Passando valores de parâmetro  
 Um aplicativo pode passar o valor para um parâmetro ou no \* *ParameterValuePtr* buffer ou com uma ou mais chamadas para **SQLPutData**. Parâmetros cujos dados são passados com **SQLPutData** são conhecidos como *dados em execução* parâmetros. Esses são normalmente usados para enviar dados para parâmetros SQL_LONGVARBINARY e SQL_LONGVARCHAR e podem ser combinados com outros parâmetros.  
  
 Para passar valores de parâmetro, um aplicativo executa a seguinte sequência de etapas:  
  
1.  Chamadas **SQLBindParameter** para cada parâmetro a associar os buffers para o valor do parâmetro (*ParameterValuePtr* argumento) e comprimento/indicador (*StrLen_or_IndPtr* argumento). Para parâmetros de dados em execução, *ParameterValuePtr* é um valor de ponteiro definido pelo aplicativo, como um número de parâmetro ou um ponteiro para dados. O valor será retornado posteriormente e pode ser usado para identificar o parâmetro.  
  
2.  Coloca os valores para parâmetros de entrada e entrada/saída no \* *ParameterValuePtr* e **StrLen_or_IndPtr* buffers:  
  
    -   Para parâmetros normais, o aplicativo coloca o valor do parâmetro no \* *ParameterValuePtr* buffer e o comprimento desse valor no **StrLen_or_IndPtr* buffer. Para obter mais informações, consulte [os valores de parâmetro de configuração](../../../odbc/reference/develop-app/setting-parameter-values.md).  
  
    -   Para parâmetros de dados em execução, o aplicativo coloca o resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro (quando chamando um driver ODBC 2.0) no **StrLen_or_IndPtr* buffer.  
  
3.  Chamadas **SQLExecute** ou **SQLExecDirect** para executar a instrução SQL.  
  
    -   Se não houver nenhum parâmetro de dados em execução, o processo é concluído.  
  
    -   Se houver quaisquer parâmetros de dados em execução, a função retornará SQL_NEED_DATA.  
  
4.  Chamadas **SQLParamData** para recuperar o valor definido pelo aplicativo especificado no *ParameterValuePtr* argumento de **SQLBindParameter** para o primeiro parâmetro de dados em execução a ser processado. **SQLParamData** retornará SQL_NEED_DATA.  
  
    > [!NOTE]  
    >  Embora os parâmetros de dados em execução se parecer com colunas de dados em execução, o valor retornado por **SQLParamData** é diferente para cada um. Parâmetros de dados em execução são parâmetros em uma instrução SQL para o qual os dados serão enviados com **SQLPutData** quando a instrução é executada com **SQLExecDirect** ou **SQLExecute**. Eles estão associados com **SQLBindParameter**. O valor retornado por **SQLParamData** é um valor de ponteiro transmitido para **SQLBindParameter** no *ParameterValuePtr* argumento. Colunas de dados em execução são colunas em um conjunto de linhas para o qual os dados serão enviados com **SQLPutData** quando uma linha é atualizada ou adicionada **SQLBulkOperations** ou atualizada com **SQLSetPos**. Eles estão associados com **SQLBindCol**. O valor retornado por **SQLParamData** é o endereço da linha a **TargetValuePtr* buffer (definido por uma chamada para **SQLBindCol**) que está sendo processada.  
  
5.  Chamadas **SQLPutData** uma ou mais vezes para enviar dados para o parâmetro. Mais de uma chamada é necessário se o valor dos dados for maior do que o \* *ParameterValuePtr* buffer especificado em **SQLPutData**; diversas chamadas para **SQLPutData**para o mesmo parâmetro são permitidas somente ao enviar dados de caractere C para uma coluna com um tipo específico de fonte de dados character, binary ou dados ou ao enviar dados binários de C para uma coluna com um caractere, binária, ou tipo de dados específico da fonte de dados.  
  
6.  Chamadas **SQLParamData** novamente para sinalizar que todos os dados foram enviados para o parâmetro.  
  
    -   Se houver mais parâmetros de dados em execução, **SQLParamData** retorna SQL_NEED_DATA e o valor definido pelo aplicativo para o próximo parâmetro de dados em execução a ser processado. O aplicativo se repete as etapas 4 e 5.  
  
    -   Se não houver parâmetros de não mais dados em execução, o processo é concluído. Se a instrução foi executada com êxito, **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO; se a falha na execução, ele retornará SQL_ERROR. Neste ponto, **SQLParamData** pode retornar qualquer SQLSTATE que pode ser retornado pela função que é usada para executar a instrução (**SQLExecDirect** ou **SQLExecute**).  
  
         Valores de saída para quaisquer parâmetros de entrada/saída ou de saída estão disponíveis no \* *ParameterValuePtr* e **StrLen_or_IndPtr* buffers depois que o aplicativo recupera todos os conjuntos de resultados gerado pela instrução.  
  
 Chamando **SQLExecute** ou **SQLExecDirect** coloca a instrução em um estado SQL_NEED_DATA. Neste ponto, o aplicativo pode chamar somente **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**, ou **SQLPutData** com a instrução ou o *identificador de conexão* associados à instrução. Se ele chamar qualquer outra função com a instrução ou a conexão associada com a instrução, a função retornará SQLSTATE HY010 (erro de sequência de função). As folhas de instrução de SQL_NEED_DATA de estado quando **SQLParamData** ou **SQLPutData** retorna um erro, **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, ou a instrução será cancelada.  
  
 Se o aplicativo chama **SQLCancel** enquanto o driver ainda precisa de dados para parâmetros de dados em execução, o driver cancela a execução de instrução; o aplicativo pode chamar **SQLExecute** ou  **SQLExecDirect** novamente.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperando parâmetros de saída transmitidos  
 Quando um aplicativo define *InputOutputType* SQL_PARAM_INPUT_OUTPUT_STREAM ou SQL_PARAM_OUTPUT_STREAM, o valor do parâmetro de saída deve ser recuperado por um ou mais chamadas para **SQLGetData**. Quando o driver tem um valor de parâmetro de saída em fluxo para retornar para o aplicativo, ele retornará SQL_PARAM_DATA_AVAILABLE em resposta a uma chamada para as seguintes funções: **SQLMoreResults**, **SQLExecute**, e **SQLExecDirect**. Um aplicativo chama **SQLParamData** para determinar qual valor de parâmetro está disponível.  
  
 Para obter mais informações sobre SQL_PARAM_DATA_AVAILABLE e parâmetros de saída em fluxo, consulte [recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-arrays-of-parameters"></a>Usando matrizes de parâmetros  
 Quando um aplicativo prepara uma instrução com marcadores de parâmetro e passa em uma matriz de parâmetros, há duas maneiras diferentes, que isso pode ser executado. É uma maneira para o driver dependem dos recursos de processamento de matriz de back-end, no qual caso toda a instrução com a matriz de parâmetros é tratado como uma unidade atômica. Oracle é um exemplo de uma fonte de dados que oferece suporte a recursos de processamento de matriz. Outra maneira de implementar esse recurso é para o driver gerar um lote de instruções SQL, uma instrução SQL para cada conjunto de parâmetros na matriz de parâmetros e executar o lote. Matrizes de parâmetros não podem ser usados com um **atualização WHERE CURRENT OF** instrução.  
  
 Quando uma matriz de parâmetros é processada, contagens de linha/conjuntos de resultados individuais (um para cada conjunto de parâmetros) podem estar disponíveis ou contagens de linhas/conjuntos de resultados podem ser acumuladas em uma. Opção o SQL_PARAM_ARRAY_ROW_COUNTS **SQLGetInfo** indica se as contagens de linha estão disponíveis para cada conjunto de parâmetros (SQL_PARC_BATCH) ou contagem de apenas uma linha está disponível (SQL_PARC_NO_BATCH).  
  
 Opção o SQL_PARAM_ARRAY_SELECTS **SQLGetInfo** indica se um conjunto de resultados está disponível para cada conjunto de parâmetros (SQL_PAS_BATCH) ou apenas um conjunto de resultados está disponível (SQL_PAS_NO_BATCH). Se o driver não permite que uma instrução de geração de conjunto de resultados a ser executado com uma matriz de parâmetros, SQL_PARAM_ARRAY_SELECTS retornará SQL_PAS_NO_SELECT.  
  
 Para obter mais informações, consulte [função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 Para dar suporte a matrizes de parâmetros, o atributo da instrução SQL_ATTR_PARAMSET_SIZE é definido para especificar o número de valores para cada parâmetro. Se o campo for maior que 1, os campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR de APD devem apontar para matrizes. A cardinalidade de cada matriz é igual ao valor de SQL_ATTR_PARAMSET_SIZE.  
  
 O campo SQL_DESC_ROWS_PROCESSED_PTR de APD aponta para um buffer que contém o número de conjuntos de parâmetros que foram processados, incluindo conjuntos de erro. Como cada conjunto de parâmetros é processado, o driver armazena um novo valor no buffer. Nenhum número será retornado se esse for um ponteiro nulo. Quando matrizes de parâmetros são usados, o valor apontado pelo campo SQL_DESC_ROWS_PROCESSED_PTR de APD é preenchido mesmo se SQL_ERROR é retornado pela função de configuração. Se SQL_NEED_DATA for retornado, o valor apontado pelo campo SQL_DESC_ROWS_PROCESSED_PTR de APD é definido como o conjunto de parâmetros que está sendo processado.  
  
 O que ocorre quando uma matriz de parâmetros está associada e uma **atualização WHERE CURRENT OF** instrução é executada é definido pelo driver.  
  
## <a name="column-wise-parameter-binding"></a>A associação de parâmetros  
 Em que a associação, o aplicativo associa parâmetros separados e matrizes de comprimento/indicador para cada parâmetro.  
  
 Para usar a associação, o aplicativo primeiro define o atributo de instrução SQL_ATTR_PARAM_BIND_TYPE como SQL_PARAM_BIND_BY_COLUMN. (Esse é o padrão). Para cada coluna a ser associado, o aplicativo executa as seguintes etapas:  
  
1.  Aloca uma matriz de buffer de parâmetros.  
  
2.  Aloca uma matriz de buffers de comprimento/indicador.  
  
    > [!NOTE]  
    >  Se o aplicativo grava descritores diretamente quando a associação é usada, matrizes separados podem ser usados para dados de comprimento e indicador.  
  
3.  Chamadas **SQLBindParameter** com os seguintes argumentos:  
  
    -   *ValueType* é o tipo C de um único elemento na matriz de buffer de parâmetros.  
  
    -   *ParameterType* é o tipo SQL do parâmetro.  
  
    -   *ParameterValuePtr* é o endereço da matriz de buffers de parâmetro.  
  
    -   *BufferLength* é o tamanho de um único elemento na matriz de buffer de parâmetros. O *BufferLength* argumento é ignorado quando os dados são dados de comprimento fixo.  
  
    -   *StrLen_or_IndPtr* é o endereço da matriz de comprimento/indicador.  
  
 Para obter mais informações sobre como essas informações são usadas, consulte "ParameterValuePtr argumento" em "Comentários", nesta seção. Para obter mais informações sobre a associação de parâmetros, consulte [matrizes de parâmetros de ligação](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="row-wise-parameter-binding"></a>A associação de parâmetros  
 Na associação, o aplicativo define uma estrutura que contém buffers de parâmetro e o comprimento/indicador para cada parâmetro a ser associado.  
  
 Para usar a associação, o aplicativo executa as seguintes etapas:  
  
1.  Define uma estrutura para conter um único conjunto de parâmetros (incluindo os buffers de parâmetro e o comprimento/indicador) e aloca uma matriz dessas estruturas.  
  
    > [!NOTE]  
    >  Se o aplicativo grava descritores diretamente quando a associação é usada, campos separados podem ser usados para dados de comprimento e indicador.  
  
2.  Define o atributo de instrução SQL_ATTR_PARAM_BIND_TYPE para o tamanho da estrutura que contém um único conjunto de parâmetros ou para o tamanho de uma instância de um buffer no qual os parâmetros serão associados. O comprimento deve incluir espaço para todos os parâmetros associados e qualquer preenchimento da estrutura ou do buffer, para certificar-se de que, quando o endereço de um parâmetro associado é incrementado com o comprimento especificado, o resultado apontará para o início do parâmetro no mesmo o próxima linha. Quando você usa o *sizeof* operador em ANSI C, esse comportamento é garantido.  
  
3.  Chamadas **SQLBindParameter** com os argumentos a seguir para cada parâmetro a ser associado:  
  
    -   *ValueType* é o tipo do membro de buffer de parâmetro a ser associado à coluna.  
  
    -   *ParameterType* é o tipo SQL do parâmetro.  
  
    -   *ParameterValuePtr* é o endereço do membro de buffer de parâmetro no primeiro elemento da matriz.  
  
    -   *BufferLength* é o tamanho do membro de buffer de parâmetro.  
  
    -   *StrLen_or_IndPtr* é o endereço do membro de comprimento/indicador a ser associado.  
  
 Para obter mais informações sobre como essas informações são usadas, consulte "*ParameterValuePtr* argumento," mais adiante nesta seção. Para obter mais informações sobre a associação de parâmetros, consulte o [matrizes de parâmetros de ligação](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="error-information"></a>Informações de erro  
 Se um driver não implementa matrizes de parâmetros como lotes (a opção SQL_PARAM_ARRAY_ROW_COUNTS é igual a SQL_PARC_NO_BATCH), situações de erro são tratadas como se uma instrução foi executada. Se o driver implementar matrizes de parâmetros como lotes, um aplicativo pode usar o campo de cabeçalho SQL_DESC_ARRAY_STATUS_PTR do IPD para determinar qual parâmetro de uma instrução SQL ou qual parâmetro em uma matriz de parâmetros causado  **SQLExecDirect** ou **SQLExecute** para retornar um erro. Este campo contém informações de status para cada linha de valores de parâmetro. Se o campo indica que ocorreu um erro, campos na estrutura de dados de diagnóstico indica o número de linhas e de parâmetro do parâmetro que falhou. O número de elementos na matriz será definido pelo campo de cabeçalho SQL_DESC_ARRAY_SIZE no APD, que pode ser definido pelo atributo de instrução SQL_ATTR_PARAMSET_SIZE.  
  
> [!NOTE]  
>  O campo de cabeçalho SQL_DESC_ARRAY_STATUS_PTR no APD é usado para ignorar os parâmetros. Para obter mais informações sobre como ignorar parâmetros, consulte a próxima seção, "Ignorando um conjunto de parâmetros".  
  
 Quando **SQLExecute** ou **SQLExecDirect** retorna SQL_ERROR, os elementos na matriz apontada pelo campo SQL_DESC_ARRAY_STATUS_PTR o IPD conterá SQL SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, _ PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED ou SQL_PARAM_DIAG_UNAVAILABLE.  
  
 Para cada elemento nesta matriz, a estrutura de dados de diagnóstico contém um ou mais registros de status. O campo SQL_DIAG_ROW_NUMBER da estrutura indica o número de linha dos valores de parâmetro que causou o erro. Se for possível determinar o parâmetro específico em uma linha de parâmetros que causou o erro, o número do parâmetro será inserido no campo SQL_DIAG_COLUMN_NUMBER.  
  
 SQL_PARAM_UNUSED é inserido quando um parâmetro não foi usado porque ocorreu um erro em um parâmetro anterior que forçado **SQLExecute** ou **SQLExecDirect** para anular. Por exemplo, se houver 50 parâmetros e um erro ao executar o fortieth conjunto de parâmetros que causou **SQLExecute** ou **SQLExecDirect** seja anulada, e SQL_PARAM_UNUSED é inserido do matriz de status para parâmetros 41 a 50.  
  
 SQL_PARAM_DIAG_UNAVAILABLE é inserido quando o driver trata matrizes de parâmetros como uma unidade monolítica, portanto ele não gera esse nível de parâmetro individual de informações de erro.  
  
 Alguns erros no processamento de um único conjunto de parâmetros fazem com que o processamento dos conjuntos de parâmetros subsequentes na matriz para parar. Outros erros não afetam o processamento de parâmetros subsequentes. Quais erros pararão o processamento é definido pelo driver. Se o processamento não for interrompido, todos os parâmetros na matriz são processados, SQL_SUCCESS_WITH_INFO será retornado como resultado de erro e o buffer definido pelo SQL_ATTR_PARAMS_PROCESSED_PTR é definido como o número total de conjuntos de parâmetros processados (conforme definido pelo Atributo de instrução SQL_ATTR_PARAMSET_SIZE), que inclui os conjuntos de erro.  
  
> [!CAUTION]  
>  Comportamento ODBC quando ocorre um erro no processamento de uma matriz de parâmetros é diferente em ODBC 3. *x* do que era no ODBC 2. *x*. No ODBC 2. *x*, a função retornou SQL_ERROR e processamento parou. O buffer apontado pelo *pirow* argumento de **para SQLParamOptions** continha o número da linha de erro. Em ODBC 3. *x*, a função retorna SQL_SUCCESS_WITH_INFO e processamento de maio ou parar ou continuar. Se você continuar, o buffer especificado por SQL_ATTR_PARAMS_PROCESSED_PTR será definido para o valor de todos os parâmetros processados, incluindo aqueles que resultou em erro. Essa alteração no comportamento pode causar problemas para os aplicativos existentes.  
  
 Quando **SQLExecute** ou **SQLExecDirect** retorna antes de concluir o processamento de todos os conjuntos de parâmetros em uma matriz de parâmetros, como quando SQL_ERROR ou SQL_NEED_DATA é retornado, contém a matriz de status status para os parâmetros que já foram processados. O local apontado pelo campo SQL_DESC_ROWS_PROCESSED_PTR o IPD contém o número de linha na matriz de parâmetros que fez com que o código de erro SQL_ERROR ou SQL_NEED_DATA. Quando uma matriz de parâmetros é enviada para uma instrução SELECT, a disponibilidade de valores de matriz de status é definido pelo driver; eles podem estar disponíveis após a instrução foi executada ou como resultado conjuntos são buscados.  
  
## <a name="ignoring-a-set-of-parameters"></a>Ignorando a um conjunto de parâmetros  
 O campo SQL_DESC_ARRAY_STATUS_PTR de APD (conforme definido pela instrução sql_attr_param_status_ptr) pode ser usado para indicar que um conjunto de parâmetros associados em uma instrução SQL deve ser ignorado. Para direcionar o driver para ignorar um ou mais conjuntos de parâmetros durante a execução, um aplicativo deve seguir estas etapas:  
  
1.  Chamar **SQLSetDescField** para definir o campo de cabeçalho SQL_DESC_ARRAY_STATUS_PTR de APD para apontar para uma matriz de valores SQLUSMALLINT para conter as informações de status. Este campo também pode ser definido chamando **SQLSetStmtAttr** com um *atributo* de SQL_ATTR_PARAM_OPERATION_PTR, que permite que um aplicativo defina o campo sem obter um identificador do descritor.  
  
2.  Defina cada elemento da matriz definida no campo SQL_DESC_ARRAY_STATUS_PTR de APD para um dos dois valores:  
  
    -   SQL_PARAM_IGNORE, para indicar que a linha foi excluída da execução da instrução.  
  
    -   SQL_PARAM_PROCEED, para indicar que a linha é incluída na execução da instrução.  
  
3.  Chamar **SQLExecDirect** ou **SQLExecute** para executar a instrução preparada.  
  
 As seguintes regras se aplicam a matriz definida pelo campo SQL_DESC_ARRAY_STATUS_PTR de APD:  
  
-   O ponteiro é definido como nulo por padrão.  
  
-   Se o ponteiro for null, todos os conjuntos de parâmetros são usados, como se todos os elementos foram definidos como SQL_ROW_PROCEED.  
  
-   A definição de um elemento para SQL_PARAM_PROCEED não garante que a operação usará esse conjunto específico de parâmetros.  
  
-   SQL_PARAM_PROCEED é definido como 0 no arquivo de cabeçalho.  
  
 Um aplicativo pode definir o campo SQL_DESC_ARRAY_STATUS_PTR no APD para apontar para o mesmo array que apontada pelo campo SQL_DESC_ARRAY_STATUS_PTR do IRD. Isso é útil quando a associação de parâmetros para dados de linha. Em seguida, podem ser ignorados parâmetros de acordo com o status dos dados da linha. Além de SQL_PARAM_IGNORE, os seguintes códigos de causam um parâmetro em uma instrução SQL para ser ignorada: SQL_ROW_DELETED, SQL_ROW_UPDATED e SQL_ROW_ERROR. Além de SQL_PARAM_PROCEED, os seguintes códigos de fazer com que uma instrução SQL continuar: SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO e SQL_ROW_ADDED.  
  
## <a name="rebinding-parameters"></a>Parâmetros de reassociação  
 Um aplicativo pode executar qualquer uma das duas operações para alterar a associação:  
  
-   Chamar **SQLBindParameter** para especificar uma nova associação para uma coluna que já está associada. O driver substituirá a associação antiga pelo novo.  
  
-   Especifique um deslocamento a ser adicionada para o endereço de buffer especificado pela chamada de associação para **SQLBindParameter**. Para obter mais informações, consulte a próxima seção, "Reassociação com deslocamentos."  
  
## <a name="rebinding-with-offsets"></a>Reassociação com deslocamentos  
 Reassociação dos parâmetros é especialmente útil quando um aplicativo tem uma configuração de área de buffer que pode conter vários parâmetros, mas uma chamada para **SQLExecDirect** ou **SQLExecute** usa apenas alguns dos parâmetros. O espaço restante na área de buffer pode ser usado para o próximo conjunto de parâmetros, modificando a associação existente por um deslocamento.  
  
 O campo de cabeçalho SQL_DESC_BIND_OFFSET_PTR no APD aponta para o deslocamento de associação. Se o campo for não nulo, o driver cancelará o ponteiro e, se nenhum dos valores nos campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR é um ponteiro nulo, adiciona o valor cancelado a esses campos no descritor de registros em tempo de execução. Os novos valores de ponteiro são usados quando as instruções SQL são executadas. O deslocamento permanece válido após reassociação. Como SQL_DESC_BIND_OFFSET_PTR é um ponteiro para o deslocamento, em vez do deslocamento em si, um aplicativo pode alterar o deslocamento diretamente, sem a necessidade de chamar [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) ou [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) para Altere o campo do descritor. O ponteiro é definido como nulo por padrão. O campo SQL_DESC_BIND_OFFSET_PTR da descartar pode ser definido por uma chamada para [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) ou por uma chamada para [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)com um *fAttribute* de SQL_ATTR_PARAM_BIND_ OFFSET_PTR.  
  
 O deslocamento de associação sempre é adicionado diretamente para os valores nos campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR. Se o deslocamento for alterado para um valor diferente, o novo valor é adicionado diretamente para o valor de cada campo do descritor. O novo deslocamento não é adicionado à soma de valor do campo e qualquer deslocamentos anteriores.  
  
## <a name="descriptors"></a>Descritores  
 Como um parâmetro está associado é determinado pelos campos de APDs e IPDs. Os argumentos em **SQLBindParameter** são usados para definir os campos de descritor. Os campos também podem ser definidos **SQLSetDescField** funções, embora **SQLBindParameter** é mais eficiente usar porque o aplicativo não precisa obter um identificador de descritor para chamar **SQLBindParameter**.  
  
> [!CAUTION]  
>  Chamando **SQLBindParameter** para uma instrução pode afetar outras instruções. Isso ocorre quando a descartar associado à instrução explicitamente é alocado e também está associado com outras instruções. Porque **SQLBindParameter** modifica os campos de APD, as modificações se aplicam a todas as instruções ao qual esse descritor está associado. Se isso não é o comportamento necessário, o aplicativo deve desassociar este descritor de outras instruções antes de chamar **SQLBindParameter**.  
  
 Conceitualmente, **SQLBindParameter** executa as seguintes etapas na sequência:  
  
1.  Chamadas [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) ao obter o identificador APD.  
  
2.  Chamadas [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) ao obter o campo SQL_DESC_COUNT do APD e se o valor da *ColumnNumber* argumento excede o valor de SQL_DESC_COUNT, chamadas **SQLSetDescField**para aumentar o valor de SQL_DESC_COUNT para *ColumnNumber*.  
  
3.  Chamadas [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) várias vezes para atribuir valores para os seguintes campos de APD:  
  
    -   Define SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE como o valor de *ValueType*, exceto que se *ValueType* é um dos identificadores de um subtipo de datetime ou intervalo de concisa, ele define SQL_DESC_TYPE para SQL _ DATETIME ou SQL_INTERVAL, respectivamente, define SQL_DESC_CONCISE_TYPE para o identificador conciso e define SQL_DESC_DATETIME_INTERVAL_CODE para datetime correspondente ou subcódigo de intervalo.  
  
    -   Define o campo SQL_DESC_OCTET_LENGTH como o valor de *BufferLength*.  
  
    -   Define o campo SQL_DESC_DATA_PTR para o valor de *ParameterValue*.  
  
    -   Define o campo SQL_DESC_OCTET_LENGTH_PTR como o valor de *StrLen_or_Ind*.  
  
    -   Define o campo SQL_DESC_INDICATOR_PTR também como o valor de *StrLen_or_Ind*.  
  
     O *StrLen_or_Ind* parâmetro especifica as informações de indicador e o comprimento do valor do parâmetro.  
  
4.  Chamadas [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) ao obter o identificador IPD.  
  
5.  Chamadas [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) ao obter o campo SQL_DESC_COUNT do IPD e se o valor da *ColumnNumber* argumento excede o valor de SQL_DESC_COUNT, chamadas **SQLSetDescField**para aumentar o valor de SQL_DESC_COUNT para *ColumnNumber*.  
  
6.  Chamadas [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) várias vezes para atribuir valores para os campos do IPD a seguir:  
  
    -   Define SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE como o valor de *ParameterType*, exceto que se *ParameterType* é um dos identificadores de um subtipo de datetime ou intervalo de concisa, ele define SQL_DESC_TYPE SQL_DATETIME ou SQL_INTERVAL, respectivamente, define SQL_DESC_CONCISE_TYPE identificador concisa e conjuntos de SQL_DESC_DATETIME_INTERVAL_CODE datetime correspondente ou subcódigo de intervalo.  
  
    -   Define um ou mais dos SQL_DESC_LENGTH, SQL_DESC_PRECISION e SQL_DESC_DATETIME_INTERVAL_PRECISION, conforme apropriado para *ParameterType*.  
  
    -   Define SQL_DESC_SCALE como o valor de *DecimalDigits*.  
  
 Se a chamada para **SQLBindParameter** falhar, o conteúdo dos campos de descritor que ele tenha definida no APD não são definidos e o campo SQL_DESC_COUNT de APD é alterado. Além disso, os campos SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_TYPE do registro apropriado no IPD são indefinidos e o campo SQL_DESC_COUNT do IPD é alterado.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>Conversão de chamadas de e para SQLSetParam  
 Quando um aplicativo ODBC 1.0 chama **SQLSetParam** em um ODBC 3. *x* driver, o ODBC 3. *x* Gerenciador de Driver mapeia a chamada, conforme mostrado na tabela a seguir.  
  
|Chamada por um aplicativo ODBC 1.0|Chamada para ODBC 3. *x* driver|  
|----------------------------------|-------------------------------|  
|SQLSetParam (StatementHandle, ParameterNumber, ValueType, ParameterType, LengthPrecision, ParameterScale, ParameterValuePtr, StrLen_or_IndPtr);|SQLBindParameter (StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, *ColumnSize*, *DecimalDigits*, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX,      StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo prepara uma instrução SQL para inserir dados na tabela ORDERS. Para cada parâmetro na instrução, o aplicativo chama **SQLBindParameter** para especificar o tipo de dados ODBC C e o tipo de dados SQL do parâmetro e para associar um buffer para cada parâmetro. Para cada linha de dados, o aplicativo atribui valores de dados para cada parâmetro e chama **SQLExecute** para executar a instrução.  
  
 O exemplo a seguir supõe que você tenha uma fonte de dados ODBC no computador chamado Northwind que está associado com o banco de dados Northwind.  
  
 Para obter mais exemplos de código, consulte [SQLBulkOperations função](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [função SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md), [função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), e [função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
// SQLBindParameter_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define EMPLOYEE_ID_LEN 10  
  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLSMALLINT sCustID;  
  
SQLCHAR szEmployeeID[EMPLOYEE_ID_LEN];  
SQL_DATE_STRUCT dsOrderDate;  
SQLINTEGER cbCustID = 0, cbOrderDate = 0, cbEmployeeID = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, EMPLOYEE_ID_LEN, 0, szEmployeeID, 0, &cbEmployeeID);  
   retcode = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sCustID, 0, &cbCustID);  
   retcode = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TIMESTAMP, sizeof(dsOrderDate), 0, &dsOrderDate, 0, &cbOrderDate);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"INSERT INTO Orders(CustomerID, EmployeeID, OrderDate) VALUES (?, ?, ?)", SQL_NTS);  
  
   strcpy_s((char*)szEmployeeID, _countof(szEmployeeID), "BERGS");  
   sCustID = 5;  
   dsOrderDate.year = 2006;  
   dsOrderDate.month = 3;  
   dsOrderDate.day = 17;  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo executa um procedimento armazenado do SQL Server usando um parâmetro nomeado.  
  
```  
// SQLBindParameter_Function_2.cpp  
// compile with: ODBC32.lib  
// sample assumes the following stored procedure:  
// use northwind  
// DROP PROCEDURE SQLBindParameter  
// GO  
//   
// CREATE PROCEDURE SQLBindParameter @quote int  
// AS  
// delete from orders where OrderID >= @quote  
// GO  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
SQLHDESC hIpd = NULL;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLCHAR szQuote[50] = "100084";  
SQLINTEGER cbValue = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"{call SQLBindParameter(?)}", SQL_NTS);  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 50, 0, szQuote, 0, &cbValue);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
   retcode = SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando informações sobre um parâmetro em uma instrução|[Função SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução preparada do SQL|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberar buffers de parâmetro na instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Retornando o número de parâmetros de instrução|[Função SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|Retornando o próximo parâmetro para enviar dados|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Especificando vários valores de parâmetro|[Função SQLParamOptions](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|Envio de dados de parâmetro em tempo de execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
