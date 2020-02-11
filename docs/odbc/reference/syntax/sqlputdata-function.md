---
title: Função SQLPutData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 676f9fb526996e96b27bb758a7343c86afaac460
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053655"
---
# <a name="sqlputdata-function"></a>Função SQLPutData
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 O **SQLPutData** permite que um aplicativo envie dados para um parâmetro ou coluna para o driver em tempo de execução da instrução. Essa função pode ser usada para enviar valores de dados binários ou de caractere em partes para uma coluna com um tipo de dados específico de caractere, binário ou de fonte de dados (por exemplo, parâmetros dos tipos SQL_LONGVARBINARY ou SQL_LONGVARCHAR). O **SQLPutData** dá suporte à associação a um tipo de dados C Unicode, mesmo que o driver subjacente não ofereça suporte a dados Unicode.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *DataPtr*  
 Entrada Ponteiro para um buffer que contém os dados reais para o parâmetro ou coluna. Os dados devem estar no tipo de dados C especificado no argumento *ValueType* de **SQLBindParameter** (para dados de parâmetro) ou no argumento *TargetType* de **SQLBindCol** (para dados de coluna).  
  
 *StrLen_or_Ind*  
 Entrada Comprimento de \* *DataPtr*. Especifica a quantidade de dados enviados em uma chamada para **SQLPutData**. A quantidade de dados pode variar com cada chamada para um determinado parâmetro ou coluna. *StrLen_or_Ind* é ignorado, a menos que ele atenda a uma das seguintes condições:  
  
-   *StrLen_or_Ind* é SQL_NTS, SQL_NULL_DATA ou SQL_DEFAULT_PARAM.  
  
-   O tipo de dados C especificado em **SQLBindParameter** ou **SQLBindCol** é SQL_C_CHAR ou SQL_C_BINARY.  
  
-   O tipo de dados C é SQL_C_DEFAULT e o tipo de dados C padrão para o tipo de dados SQL especificado é SQL_C_CHAR ou SQL_C_BINARY.  
  
 Para todos os outros tipos de dados C, se *StrLen_or_Ind* não for SQL_NULL_DATA ou SQL_DEFAULT_PARAM, o driver pressupõe que o tamanho do \*buffer *DataPtr* é o tamanho do tipo de dados C especificado com *ValueType* ou *TargetType* e envia o valor de dados inteiro. Para obter mais informações, consulte [convertendo dados de tipos de dados C para SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) no Apêndice D: tipos de dados.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLPutData** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLPutData** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|Dados de cadeia de caracteres ou binários retornados para um parâmetro de saída resultaram no truncamento de um caractere não em branco ou dados binários não nulos. Se fosse um valor de cadeia de caracteres, ele foi truncado à direita. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O valor de dados identificado pelo argumento *ValueType* em **SQLBindParameter** para o parâmetro associado não pôde ser convertido para o tipo de dados identificado pelo argumento *ParameterType* em **SQLBindParameter**.|  
|07S01|Uso inválido do parâmetro padrão|Um valor de parâmetro, definido com **SQLBindParameter**, foi SQL_DEFAULT_PARAM e o parâmetro correspondente não tinha um valor padrão.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|22001|Dados de cadeia de caracteres, truncamento à direita|A atribuição de um valor de caractere ou binário a uma coluna resultou no truncamento de caracteres ou bytes não vazios (caracteres) ou não nulos (binários).<br /><br /> O tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo** era "Y" e mais dados foram enviados para um parâmetro longo (o tipo de dados era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico da fonte de dados longa) do que foi especificado com o argumento *StrLen_or_IndPtr* em **SQLBindParameter**.<br /><br /> O tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo** era "Y" e mais dados foram enviados para uma coluna longa (o tipo de dados era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico da fonte de dados longa) do que foi especificado no buffer de comprimento correspondente a uma coluna em uma linha de dados que foi adicionada ou atualizada com **SQLBulkOperations** ou atualizada com **SQLSetPos**.|  
|22003|Valor numérico fora do intervalo|Os dados enviados para uma coluna ou parâmetro numérico associado fizeram com que a parte inteira (em oposição à fracionária) do número seja truncada quando atribuída à coluna da tabela associada.<br /><br /> Retornar um valor numérico (como numérico ou cadeia de caracteres) para um ou mais parâmetros de entrada/saída ou saída teria causado a parte inteira (em oposição à fracionária) do número a ser truncado.|  
|22007|Formato de data e hora inválido|Os dados enviados para um parâmetro ou coluna que foi associado a uma estrutura de data, hora ou timestamp era, respectivamente, uma data, hora ou carimbo de hora inválido.<br /><br /> Um parâmetro de entrada/saída ou de saída foi associado a uma estrutura C de data, hora ou timestamp, e um valor no parâmetro retornado foi, respectivamente, uma data, hora ou carimbo de hora inválido. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|22008|Estouro no campo DateTime|Uma expressão DateTime computada para um parâmetro de entrada/saída ou de saída resultou em uma estrutura C de data, hora ou timestamp que era inválida.|  
|22012|Divisão por zero|Uma expressão aritmética calculada para um parâmetro de entrada/saída ou saída resultou em divisão por zero.|  
|22015|Estouro no campo de intervalo|Os dados enviados para uma coluna ou parâmetro numérico exato ou de intervalo para um tipo de dados SQL de intervalo causaram uma perda de dígitos significativos.<br /><br /> Os dados foram enviados para uma coluna de intervalo ou parâmetro com mais de um campo, foram convertidos em um tipo de dados numérico e não tinham nenhuma representação no tipo de dados numeric.<br /><br /> Os dados enviados para a coluna ou dados de parâmetro foram atribuídos a um tipo SQL de intervalo, e não havia nenhuma representação do valor do tipo C no tipo SQL de intervalo.<br /><br /> Os dados enviados para uma coluna exata numérica ou de intervalo C ou parâmetro para um tipo de intervalo C causaram uma perda de dígitos significativos.<br /><br /> Os dados enviados para a coluna ou dados de parâmetro foram atribuídos a uma estrutura C de intervalo e não havia nenhuma representação dos dados na estrutura de dados do intervalo.|  
|22018|Valor de caractere inválido para especificação de conversão|O tipo C era um tipo de dados numérico exato ou aproximado, um DateTime ou um intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna ou no parâmetro não era um literal válido do tipo ligado de C.<br /><br /> O tipo SQL era um tipo de dados numérico exato ou aproximado, um DateTime ou um intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna ou no parâmetro não era um literal válido do tipo SQL associado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|(DM) o argumento *DataPtr* era um ponteiro nulo e o argumento *StrLen_or_Ind* não era 0, SQL_DEFAULT_PARAM ou SQL_NULL_DATA.|  
|HY010|Erro de sequência de função|(DM) a chamada de função anterior não era uma chamada para **SQLPutData** ou **SQLParamData**.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função SQLPutData foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY019|Dados não caracteres e não binários enviados em partes|**SQLPutData** foi chamado mais de uma vez para um parâmetro ou coluna, e ele não estava sendo usado para enviar dados c de caracteres para uma coluna com um tipo de dados específico de caractere, binário ou de fonte de dados ou para enviar dados binários c para uma coluna com um tipo de dados de caractere, binário ou específico de fonte de dados.|  
|HY020|Tentativa de concatenar um valor nulo|**SQLPutData** foi chamado mais de uma vez, pois a chamada retornada SQL_NEED_DATA e em uma dessas chamadas, o argumento *StrLen_or_Ind* continha SQL_NULL_DATA ou SQL_DEFAULT_PARAM.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|O argumento *DataPtr* não era um ponteiro nulo e o argumento *StrLen_or_Ind* era menor que 0, mas não é igual a SQL_NTS ou SQL_NULL_DATA.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
 Se **SQLPutData** for chamado durante o envio de dados para um parâmetro em uma instrução SQL, ele poderá retornar qualquer SQLSTATE que possa ser retornado pela função chamada para executar a instrução (**SQLExecute** ou **SQLExecDirect**). Se for chamado durante o envio de dados para uma coluna sendo atualizada ou adicionada com **SQLBulkOperations** ou atualizada com **SQLSetPos**, ela poderá retornar qualquer SQLSTATE que possa ser retornado por **SQLBulkOperations** ou **SQLSetPos**.  
  
## <a name="comments"></a>Comentários  
 **SQLPutData** pode ser chamado para fornecer dados em execução para dois usos: dados de parâmetro a serem usados em uma chamada para **SQLExecute** ou **SQLExecDirect**, ou dados de coluna a serem usados quando uma linha é atualizada ou adicionada por uma chamada para **SQLBulkOperations** ou é atualizada por uma chamada para **SQLSetPos**.  
  
 Quando um aplicativo chama **SQLParamData** para determinar quais dados ele deve enviar, o driver retorna um indicador que o aplicativo pode usar para determinar quais dados de parâmetro enviar ou onde os dados da coluna podem ser encontrados. Ele também retorna SQL_NEED_DATA, que é um indicador para o aplicativo que ele deve chamar **SQLPutData** para enviar os dados. No argumento *DataPtr* para **SQLPutData**, o aplicativo passa um ponteiro para o buffer que contém os dados reais para o parâmetro ou coluna.  
  
 Quando o driver retorna SQL_SUCCESS para **SQLPutData**, o aplicativo chama **SQLParamData** novamente. **SQLParamData** retornará SQL_NEED_DATA se for necessário enviar mais dados, caso em que o aplicativo chama **SQLPutData** novamente. Ele retornará SQL_SUCCESS se todos os dados em execução forem enviados. O aplicativo então chama **SQLParamData** novamente. Se o driver retornar SQL_NEED_DATA e outro indicador em * \*ValuePtrPtr*, ele exigirá dados para outro parâmetro ou coluna e **SQLPutData** será chamado novamente. Se o driver retornar SQL_SUCCESS, todos os dados em execução serão enviados e a instrução SQL poderá ser executada, ou a chamada **SQLBulkOperations** ou **SQLSetPos** poderá ser processada.  
  
 Para obter mais informações sobre como os dados de parâmetro de dados em execução são passados no momento da execução da instrução, consulte "passando valores de parâmetro" em [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [enviando dados longos](../../../odbc/reference/develop-app/sending-long-data.md). Para obter mais informações sobre como os dados de coluna de dados em execução são atualizados ou adicionados, consulte a seção "usando SQLSetPos" em [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "executando atualizações em massa usando indicadores" em [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)e [Long data e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
> [!NOTE]  
>  Um aplicativo pode usar **SQLPutData** para enviar dados somente em partes ao enviar dados de caractere C para uma coluna com um tipo de dados específico de fonte de dados, binário ou de caractere ou ao enviar dados binários c para uma coluna com um tipo de dados de caractere, binário ou específico de fonte de dados. Se **SQLPutData** for chamado mais de uma vez em qualquer outra condição, ele retornará SQL_ERROR e SQLSTATE HY019 (dados não caracteres e não binários enviados em partes).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir pressupõe um nome de fonte de dados chamado Test. O banco de dados associado deve ter uma tabela que você pode criar, da seguinte maneira:  
  
```sql  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```cpp  
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
|Associando um buffer a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando o próximo parâmetro para o qual enviar dados|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
