---
title: Função SQLPutData | Microsoft Docs
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
- SQLPutData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPutData
helpviewer_keywords:
- SQLPutData function [ODBC]
ms.assetid: 9a60f004-1477-4c54-a20c-7378e1116713
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e612ac7a6df03349f7cf00eb83433a86556cf8b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlputdata-function"></a>Função SQLPutData
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLPutData** permite que um aplicativo enviar dados para uma coluna ou parâmetro para o driver no tempo de execução de instrução. Essa função pode ser usada para enviar caracteres ou valores de dados binários em partes para uma coluna com um tipo específico de fonte de dados character, binary ou dados (por exemplo, os parâmetros dos tipos de SQL_LONGVARBINARY ou SQL_LONGVARCHAR). **SQLPutData** dá suporte à associação a um tipo de dados Unicode C, mesmo que o driver subjacente não oferece suporte a dados Unicode.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *DataPtr*  
 [Entrada] Ponteiro para um buffer que contém os dados reais para o parâmetro ou coluna. Os dados devem estar no tipo de dados C especificado no *ValueType* argumento de **SQLBindParameter** (para os dados de parâmetro) ou o *TargetType* argumento de  **SQLBindCol** (para dados de coluna).  
  
 *StrLen_or_Ind*  
 [Entrada] Comprimento de \* *DataPtr*. Especifica a quantidade de dados enviados em uma chamada para **SQLPutData**. A quantidade de dados pode variar com cada chamada para um determinado parâmetro ou coluna. *StrLen_or_Ind* é ignorado, a menos que ele atenda a uma das seguintes condições:  
  
-   *StrLen_or_Ind* é SQL_NTS, SQL_NULL_DATA ou SQL_DEFAULT_PARAM.  
  
-   O tipo de dados C especificado em **SQLBindParameter** ou **SQLBindCol** é SQL_C_CHAR ou SQL_C_BINARY.  
  
-   O tipo de dados C é SQL_C_DEFAULT, e o tipo de dados C padrão para o tipo de dados SQL especificado é SQL_C_CHAR ou SQL_C_BINARY.  
  
 Todos os outros tipos de dados C, se *StrLen_or_Ind* não é SQL_NULL_DATA ou SQL_DEFAULT_PARAM, o driver pressupõe que o tamanho do \* *DataPtr* buffer é o tamanho do tipo de dados C especificado com *ValueType* ou *TargetType* e envia o valor de dados inteiro. Para obter mais informações, consulte [converter dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) no Apêndice d: os tipos de dados.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLPutData** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLPutData** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Cadeia de caracteres ou dados binários retornados para um parâmetro de saída resultaram em truncamento de caracteres não vazia ou dados binários não nulo. Se fosse um valor de cadeia de caracteres, foi truncado à direita. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|O valor de dados identificado pelo *ValueType* argumento **SQLBindParameter** para o parâmetro associado não pôde ser convertido para o tipo de dados identificado pelo *ParameterType*argumento **SQLBindParameter**.|  
|07S01|Uso inválido de parâmetro padrão|Um valor de parâmetro definido com **SQLBindParameter**, era SQL_DEFAULT_PARAM, e o parâmetro correspondente não tem um valor padrão.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|22001|Dados de cadeia de caracteres, truncamento à direita|A atribuição de um caractere ou valor binário para uma coluna resultou em truncamento de não vazio (caractere) ou caracteres (binários) não nulo ou bytes.<br /><br /> O tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo** foi "Y", e mais dados foi enviados para um parâmetro de tempo (o tipo de dados foi SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados de específico de fonte de dados longos) que foi especificada com o *StrLen_or_IndPtr* argumento **SQLBindParameter**.<br /><br /> O tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo** foi "Y", e mais dados foi enviados para uma coluna longa (o tipo de dados foi SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados de específico de fonte de dados longos) que foi especificada no buffer de comprimento correspondente a uma coluna em uma linha de dados que foram adicionados ou atualizados com **SQLBulkOperations** ou atualizada com **SQLSetPos**.|  
|22003|Valor numérico fora do intervalo|Os dados enviados para um parâmetro numérico associado ou coluna causou a parte inteira (em vez de frações) o número a ser truncado quando atribuído à coluna de tabela associada.<br /><br /> Retornar um valor numérico (como numérico ou cadeia de caracteres) para um ou mais parâmetros de entrada/saída ou saídos teria causado parte inteira (em vez de frações) o número a ser truncado.|  
|22007|Formato de datetime inválido|Os dados enviados para um parâmetro ou uma coluna que foi associada a uma data, hora ou estrutura de carimbo de hora foi, respectivamente, uma data inválida, hora ou carimbo de hora.<br /><br /> Um parâmetro de entrada/saída ou de saída foi associado a uma data, hora ou estrutura de carimbo de hora C, e um valor do parâmetro retornado foi, respectivamente, uma data inválida, hora ou carimbo de hora. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|22008|Estouro no campo de data e hora|Uma expressão de data e hora é calculado para uma entrada/saída ou parâmetro de saída resultou em uma data, hora ou estrutura de carimbo de hora C que era inválida.|  
|22012|Divisão por zero|Uma expressão aritmética calculado para uma entrada/saída ou parâmetro de saída que resultou na divisão por zero.|  
|22015|Estouro no campo de intervalo|Os dados enviados para uma coluna de intervalo ou numérico exata ou o parâmetro para um tipo de dados SQL intervalo causou uma perda de dígitos significativos.<br /><br /> Dados foi enviados para um parâmetro com mais de um campo ou coluna de intervalo, foi convertidos em um tipo de dados numéricos e não tinham nenhuma representação no tipo de dados numérico.<br /><br /> Os dados enviados para a coluna ou dados de parâmetro foi atribuídos a um intervalo de tipo de SQL e não houve nenhuma representação do valor do tipo C no intervalo de tipo SQL.<br /><br /> Os dados enviados para um numérico exato ou a coluna de intervalo C ou o parâmetro para um tipo de intervalo C causou uma perda de dígitos significativos.<br /><br /> Os dados enviados para a coluna ou dados de parâmetro foi atribuídos a uma estrutura de intervalo C, e não houve nenhuma representação dos dados na estrutura de dados de intervalo.|  
|22018|Valor de caractere inválido para especificação de coerção|O tipo C foi um numérico exato ou aproximado, uma data e hora ou um tipo de dados do intervalo; o tipo SQL da coluna era de um tipo de dados de caractere; e o valor na coluna ou parâmetro não era um literal válido do tipo C associado.<br /><br /> O tipo de SQL foi um numérico exato ou aproximado, uma data e hora ou um tipo de dados do intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna ou parâmetro não era um literal válido do tipo SQL associado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em uma aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|(DM) o argumento *DataPtr* era um ponteiro nulo e o argumento *StrLen_or_Ind* não era 0, SQL_DEFAULT_PARAM ou SQL_NULL_DATA.|  
|HY010|Erro de sequência de função|(DM) da chamada de função anterior não era uma chamada para **SQLPutData** ou **SQLParamData**.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando a função SQLPutData foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY019|Dados não caracteres e não binários enviados em partes|**SQLPutData** foi chamado mais de uma vez para uma coluna ou parâmetro e não estava sendo usado para enviar dados de caractere C para uma coluna com um tipo específico de fonte de dados character, binary ou dados ou para enviar dados binários de C para uma coluna com um caractere , binário ou tipo de dados específico da fonte de dados.|  
|HY020|Tentativa de concatenar um valor nulo|**SQLPutData** foi chamado mais de uma vez desde a chamada que retornou SQL_NEED_DATA e em uma dessas chamadas, o *StrLen_or_Ind* argumento contido SQL_NULL_DATA ou SQL_DEFAULT_PARAM.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|O argumento *DataPtr* não era um ponteiro nulo e o argumento *StrLen_or_Ind* era menor que 0 mas não igual a SQL_NTS ou SQL_NULL_DATA.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
 Se **SQLPutData** é chamado durante o envio de dados para um parâmetro em uma instrução SQL, ele pode retornar qualquer SQLSTATE que pode ser retornado pela função chamada para executar a instrução (**SQLExecute** ou **SQLExecDirect**). Se ele é chamado durante o envio de dados de uma coluna que está sendo atualizada ou adicionadas **SQLBulkOperations** ou que está sendo atualizado com **SQLSetPos**, pode retornar qualquer SQLSTATE que pode ser retornado por  **SQLBulkOperations** ou **SQLSetPos**.  
  
## <a name="comments"></a>Comentários  
 **SQLPutData** pode ser chamado para fornecer dados de dados em execução para dois usos: dados de parâmetro a serem usados em uma chamada para **SQLExecute** ou **SQLExecDirect**, ou dados da coluna a ser usado quando uma linha é atualizada ou adicionadas por uma chamada para **SQLBulkOperations** ou é atualizada por uma chamada para **SQLSetPos**.  
  
 Quando um aplicativo chama **SQLParamData** para determinar quais dados devem enviar, o driver retorna um indicador de que o aplicativo pode usar para determinar quais dados de parâmetro para enviar ou onde os dados da coluna podem ser encontrados. Ele também retorna SQL_NEED_DATA, que é um indicador para o aplicativo deve chamar **SQLPutData** para enviar os dados. No *DataPtr* argumento **SQLPutData**, o aplicativo passa um ponteiro para o buffer que contém os dados reais para o parâmetro ou coluna.  
  
 Quando o driver retorna SQL_SUCCESS para **SQLPutData**, o aplicativo chama **SQLParamData** novamente. **SQLParamData** retorna SQL_NEED_DATA se precisam de mais dados a ser enviada, caso em que o aplicativo chama **SQLPutData** novamente. Retorna SQL_SUCCESS se todos os dados de dados em execução foi enviado. O aplicativo chama **SQLParamData** novamente. Se o driver retorna SQL_NEED_DATA e outro indicador em  *\*ValuePtrPtr*, ele requer dados para outro parâmetro ou coluna e **SQLPutData** é chamado novamente. Se o driver retorna SQL_SUCCESS, em seguida, todos os dados em execução os dados foram enviados e a instrução SQL pode ser executada ou o **SQLBulkOperations** ou **SQLSetPos** chamada pode ser processada.  
  
 Para obter mais informações sobre os dados de parâmetro como dados em execução são passadas em tempo de execução de instrução, consulte "Valores de parâmetro passando" [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [enviar dados longos](../../../odbc/reference/develop-app/sending-long-data.md). Para obter mais informações sobre dados de coluna de dados em execução como são atualizadas ou adicionadas, consulte a seção "Usando SQLSetPos" [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Executar em massa atualizações usando indicadores" [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), e [Dados longos e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
> [!NOTE]  
>  Um aplicativo pode usar **SQLPutData** para enviar dados em partes somente ao enviar dados de caractere C para uma coluna com um tipo específico de fonte de dados character, binary ou dados ou ao enviar dados binários de C para uma coluna com um caractere, binária, ou dados tipo de dados de origem específico. Se **SQLPutData** é chamado mais de uma vez em outras condições, ela retorna SQL_ERROR e SQLSTATE HY019 (não caracteres e não binários de dados enviados em partes).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir pressupõe um nome de fonte de dados chamado teste. O banco de dados associado deve ter uma tabela que você pode criar, da seguinte maneira:  
  
```  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```  
// SQLPutData.cpp  
// compile with: odbc32.lib user32.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define TEXTSIZE  12000  
#define MAXBUFLEN 256  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // SQLBindParameter variables.  
   SQLLEN cbTextSize, lbytes;  
  
   // SQLParamData variable.  
   PTR pParmID;  
  
   // SQLPutData variables.  
   UCHAR  Data[] =   
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyz";  
  
   SDWORD cbBatch = (SDWORD)sizeof(Data) - 1;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle(hstmt1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set parameters based on total data to send.  
   lbytes = (SDWORD)TEXTSIZE;  
   cbTextSize = SQL_LEN_DATA_AT_EXEC(lbytes);  
  
   // Bind the parameter marker.  
   retcode = SQLBindParameter (hstmt1,           // hstmt  
                               1,                // ipar  
                               SQL_PARAM_INPUT,  // fParamType  
                               SQL_C_CHAR,       // fCType  
                               SQL_LONGVARCHAR,  // FSqlType  
                               lbytes,           // cbColDef  
                               0,                // ibScale  
                               (VOID *)1,        // rgbValue  
                               0,                // cbValueMax  
                               &cbTextSize);     // pcbValue  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the command.  
   retcode =   
      SQLExecDirect(hstmt1, (UCHAR*)"INSERT INTO emp4 VALUES('Paul Borm', 46,'1950-11-12 00:00:00', ?)", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_NEED_DATA) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Check to see if NEED_DATA; if yes, use SQLPutData.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if (retcode == SQL_NEED_DATA) {  
      while (lbytes > cbBatch) {  
         SQLPutData(hstmt1, Data, cbBatch);  
         lbytes -= cbBatch;  
      }  
      // Put final batch.  
      retcode = SQLPutData(hstmt1, Data, lbytes);   
   }  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Make final SQLParamData call.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("Final SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clean up.  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução preparada do SQL|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando o próximo parâmetro para enviar dados|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
