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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c4e704d96924942812904ea63d0e3d4fce8748e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300036"
---
# <a name="sqlputdata-function"></a>Função SQLPutData
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLPutData** permite que um aplicativo envie dados para um parâmetro ou coluna para o driver no momento da execução da declaração. Essa função pode ser usada para enviar valores de dados de caracteres ou binários em partes para uma coluna com um tipo de dados específico de origem de caracteres, binários ou de origem de dados (por exemplo, parâmetros dos SQL_LONGVARBINARY ou SQL_LONGVARCHAR tipos). **O SQLPutData** suporta vinculação a um tipo de dados Unicode C, mesmo que o driver subjacente não suporte dados Unicode.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *DataPtr*  
 [Entrada] Ponteiro para um buffer contendo os dados reais para o parâmetro ou coluna. Os dados devem estar no tipo de dados C especificado no argumento *ValueType* do **SQLBindParameter** (para dados de parâmetros) ou no argumento *TargetType* do **SQLBindCol** (para dados de coluna).  
  
 *StrLen_or_Ind*  
 [Entrada] Comprimento \*do *DataPtr*. Especifica a quantidade de dados enviados em uma chamada para **SQLPutData**. A quantidade de dados pode variar de acordo com cada chamada para um determinado parâmetro ou coluna. *StrLen_or_Ind* é ignorada a menos que atenda a uma das seguintes condições:  
  
-   *StrLen_or_Ind* é SQL_NTS, SQL_NULL_DATA ou SQL_DEFAULT_PARAM.  
  
-   O tipo de dados C especificado no **SQLBindParameter** ou **SQLBindCol** é SQL_C_CHAR ou SQL_C_BINARY.  
  
-   O tipo de dados C é SQL_C_DEFAULT, e o tipo de dados C padrão para o tipo de dados SQL especificado é SQL_C_CHAR ou SQL_C_BINARY.  
  
 Para todos os outros tipos de dados C, se *StrLen_or_Ind* não for \*SQL_NULL_DATA ou SQL_DEFAULT_PARAM, o driver assume que o tamanho do buffer *DataPtr* é o tamanho do tipo de dados C especificado com *ValueType* ou *TargetType* e envia todo o valor de dados. Para obter mais informações, [consulte Convertendo Dados de C para Tipos de Dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) no apêndice D: Tipos de dados.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLPutData** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLPutData** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|Dados de seqüência ou binário retornados para um parâmetro de saída resultaram na truncação de caracteres não em branco ou dados binários não-NULOS. Se fosse um valor de corda, era truncado. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O valor de dados identificado pelo argumento *ValueType* no **SQLBindParameter** para o parâmetro bound não pôde ser convertido para o tipo de dados identificado pelo argumento *ParameterType* no **SQLBindParameter**.|  
|07S01|Uso inválido de parâmetro padrão|Um valor de parâmetro, definido com **SQLBindParameter,** foi SQL_DEFAULT_PARAM, e o parâmetro correspondente não tinha um valor padrão.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|22001|Dados de cordas, truncação direita|A atribuição de um caractere ou valor binário para uma coluna resultou na truncação de caracteres ou bytes não em branco (caractere) ou não nulos (binários).<br /><br /> O SQL_NEED_LONG_DATA_LEN tipo de informação no **SQLGetInfo** era "Y", e mais dados foram enviados para um parâmetro longo (o tipo de dados era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico de origem de dados longo) do que foi especificado com o *argumento StrLen_or_IndPtr* no **SQLBindParameter**.<br /><br /> O SQL_NEED_LONG_DATA_LEN tipo de informação no **SQLGetInfo** era "Y", e mais dados foram enviados para uma coluna longa (o tipo de dados era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um longo tipo de dados específicos de origem de dados) do que foi especificado no buffer de comprimento correspondente a uma coluna em uma linha de dados que foi adicionado ou atualizado com **SQLBulkOperations** ou atualizado com **SQLSetPos**.|  
|22003|Valor numérico fora do alcance|Os dados enviados para um parâmetro numérico vinculado ou coluna fizeram com que a parte total (em oposição a fracionária) do número fosse truncada quando atribuída à coluna de tabela associada.<br /><br /> Devolver um valor numérico (como numérico ou string) para um ou mais parâmetros de entrada/saída ou de saída teria causado a truncada a parte inteira (em oposição ao fracionado) do número.|  
|22007|Formato de data-hora inválido|Os dados enviados para um parâmetro ou coluna que estava vinculado a uma data, hora ou estrutura de carimbo de data eram, respectivamente, uma data, hora ou carimbo de data inválidos.<br /><br /> Um parâmetro de entrada/saída ou saída foi vinculado a uma estrutura de data, hora ou carimbo de data C, e um valor no parâmetro retornado foi, respectivamente, uma data, hora ou carimbo de data inválido. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|22008|Estouro do campo datetime|Uma expressão de data-hora calculada para um parâmetro de entrada/saída ou saída resultou em uma estrutura de data, hora ou carimbo de ponto de data C inválida.|  
|22012|Divisão por zero|Uma expressão aritmética calculada para um parâmetro de entrada/saída ou de saída resultou em divisão por zero.|  
|22015|Estouro do campo de intervalo|Os dados enviados para uma coluna numérica exata ou parâmetro de intervalo para um tipo de dados SQL intervalado causaram uma perda de dígitos significativos.<br /><br /> Os dados foram enviados para uma coluna de intervalo ou parâmetro com mais de um campo, foram convertidos para um tipo de dados numérico e não apresentaram representação no tipo de dados numéricos.<br /><br /> Os dados enviados para dados de coluna ou parâmetro foram atribuídos a um tipo SQL de intervalo, e não houve representação do valor do tipo C no tipo SQL de intervalo.<br /><br /> Os dados enviados para uma coluna ou parâmetro exato numérico ou intervalo C para um tipo de intervalo C causaram uma perda de dígitos significativos.<br /><br /> Os dados enviados para dados de coluna ou parâmetro foram atribuídos a uma estrutura de intervalo C, e não houve representação dos dados na estrutura de dados do intervalo.|  
|22018|Valor de caractere inválido para especificação do elenco|O tipo C era um numérico exato ou aproximado, um período de data ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caracteres; e o valor na coluna ou parâmetro não era um literal válido do tipo C ligado.<br /><br /> O tipo SQL era um numérico exato ou aproximado, um período de data ou um tipo de dados de intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna ou parâmetro não era um literal válido do tipo SQL vinculado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY009|Uso inválido do ponteiro nulo|(DM) O argumento *DataPtr* era um ponteiro nulo, e o argumento *StrLen_or_Ind* não era 0, SQL_DEFAULT_PARAM ou SQL_NULL_DATA.|  
|HY010|Erro de seqüência de função|(DM) A chamada de função anterior não era uma chamada para **SQLPutData** ou **SQLParamData**.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função SQLPutData foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY019|Dados não-caracteres e não binários enviados em pedaços|**O SQLPutData** foi chamado mais de uma vez por um parâmetro ou coluna, e não estava sendo usado para enviar dados c de caracteres para uma coluna com um tipo de dados específico de origem de caracteres, binários ou de origem de dados ou para enviar dados c binários para uma coluna com um tipo de dados específico de origem de caracteres, binários ou de origem de dados.|  
|HY020|Tentativa de concatenar um valor nulo|**SQLPutData** foi chamado mais de uma vez desde que a chamada retornou SQL_NEED_DATA, e em uma dessas chamadas, o argumento *StrLen_or_Ind* continha SQL_NULL_DATA ou SQL_DEFAULT_PARAM.|  
|HY090|Comprimento de seqüência ou buffer inválido|O argumento *DataPtr* não era um ponteiro nulo, e o argumento *StrLen_or_Ind* era menor que 0, mas não era igual a SQL_NTS ou SQL_NULL_DATA.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
 Se **o SQLPutData** for chamado enquanto envia dados para um parâmetro em uma declaração SQL, ele poderá retornar qualquer SQLSTATE que possa ser retornado pela função chamada para executar a declaração **(SQLExecute** ou **SQLExecDirect).** Se for chamado durante o envio de dados para uma coluna que está sendo atualizada ou adicionada com **sqlBulkOperations** ou sendo atualizada com **SQLSetPos,** ela pode retornar qualquer SQLSTATE que possa ser retornado por **SQLBulkOperations** ou **SQLSetPos**.  
  
## <a name="comments"></a>Comentários  
 **O SQLPutData** pode ser chamado para fornecer dados de execução de dados para dois usos: dados de parâmetros a serem usados em uma chamada para **SQLExecute** ou **SQLExecDirect,** ou dados de coluna a serem usados quando uma linha é atualizada ou adicionada por uma chamada para **SQLBulkOperations** ou é atualizada por uma chamada para **SQLSetPos**.  
  
 Quando um aplicativo liga para **o SQLParamData** para determinar quais dados ele deve enviar, o driver retorna um indicador que o aplicativo pode usar para determinar quais dados de parâmetros enviar ou onde os dados da coluna podem ser encontrados. Ele também retorna SQL_NEED_DATA, que é um indicador para o aplicativo que ele deve chamar **SQLPutData** para enviar os dados. No argumento *DataPtr* para **SQLPutData,** o aplicativo passa um ponteiro para o buffer contendo os dados reais para o parâmetro ou coluna.  
  
 Quando o driver retorna SQL_SUCCESS para **SQLPutData,** o aplicativo chama **SQLParamData** novamente. **O SQLParamData** retorna SQL_NEED_DATA se mais dados precisarem ser enviados, nesse caso o aplicativo chama **sQLPutData** novamente. Ele retorna SQL_SUCCESS se todos os dados em execução forem enviados. Em seguida, o aplicativo chama **sqlParamData** novamente. Se o driver retornar SQL_NEED_DATA e outro indicador no * \*ValuePtrPtr,* ele requer dados para outro parâmetro ou coluna e **SQLPutData** é chamado novamente. Se o driver retornar SQL_SUCCESS, todos os dados em execução foram enviados e a declaração SQL pode ser executada ou a chamada **SQLBulkOperations** ou **SQLSetPos** pode ser processada.  
  
 Para obter mais informações sobre como os dados dos parâmetros de execução são passados no momento da execução da declaração, consulte "Valores de parâmetro de passagem" no [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [no envio de dados longos](../../../odbc/reference/develop-app/sending-long-data.md). Para obter mais informações sobre como os dados da coluna de execução são atualizados ou adicionados, consulte a seção "Usando SQLSetPos" em [SQLSetPos,](../../../odbc/reference/syntax/sqlsetpos-function.md)"Realizando atualizações em massa usando marcadores" em [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)e [Long Data e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
> [!NOTE]  
>  Um aplicativo pode usar **o SQLPutData** para enviar dados em partes apenas ao enviar dados c de caracteres para uma coluna com um tipo de dados específico de origem de caracteres, binários ou de origem de dados ou ao enviar dados C binários para uma coluna com um tipo de dados específico de origem de caracteres, binários ou de origem de dados. Se **o SQLPutData** for chamado mais de uma vez sob quaisquer outras condições, ele retorna SQL_ERROR e SQLSTATE HY019 (dados não-caracteres e não-binários enviados em pedaços).  
  
## <a name="example"></a>Exemplo  
 A amostra a seguir assume um nome de origem de dados chamado Teste. O banco de dados associado deve ter uma tabela que você pode criar, da seguinte forma:  
  
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
|Vinculando um buffer a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executando uma declaração SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando o próximo parâmetro para enviar dados para|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
