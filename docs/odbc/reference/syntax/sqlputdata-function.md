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
manager: craigg
ms.openlocfilehash: 5254b7bb3744e06dae300f33ff1b612b4aca2341
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537265"
---
# <a name="sqlputdata-function"></a>Função SQLPutData
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLPutData** permite que um aplicativo enviar dados para uma coluna ou parâmetro para o driver durante o tempo de execução de instrução. Essa função pode ser usada para enviar caracteres ou valores de dados binários em partes para uma coluna com um tipo específico de fonte de dados character, binary ou dados (por exemplo, os parâmetros dos tipos SQL_LONGVARBINARY ou SQL_LONGVARCHAR). **SQLPutData** dá suporte à associação a um tipo de dados C Unicode, mesmo se o driver subjacente não oferece suporte a dados Unicode.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *DataPtr*  
 [Entrada] Ponteiro para um buffer que contém os dados reais para o parâmetro ou coluna. Os dados devem estar no tipo de dados C especificado na *ValueType* argumento de **SQLBindParameter** (para dados de parâmetro) ou o *TargetType* argumento de  **SQLBindCol** (para dados de coluna).  
  
 *StrLen_or_Ind*  
 [Entrada] Comprimento da \* *DataPtr*. Especifica a quantidade de dados enviados em uma chamada para **SQLPutData**. A quantidade de dados pode variar de acordo com cada chamada para um determinado parâmetro ou coluna. *StrLen_or_Ind* é ignorado, a menos que ele atende às seguintes condições:  
  
-   *StrLen_or_Ind* é SQL_NTS, SQL_NULL_DATA ou SQL_DEFAULT_PARAM.  
  
-   O tipo de dados C especificado na **SQLBindParameter** ou **SQLBindCol** é SQL_C_CHAR ou SQL_C_BINARY.  
  
-   O tipo de dados C é SQL_C_DEFAULT e o tipo de dados C padrão para o tipo de dados SQL especificado é SQL_C_CHAR ou SQL_C_BINARY.  
  
 Para todos os outros tipos de dados de C, se *StrLen_or_Ind* não é SQL_NULL_DATA ou SQL_DEFAULT_PARAM, o driver pressupõe que o tamanho do \* *DataPtr* buffer é o tamanho do tipo de dados C especificado com o *ValueType* ou *TargetType* e envia o valor de dados inteiro. Para obter mais informações, consulte [conversão de dados do C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) no Apêndice d: Tipos de dados.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLPutData** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLPutData** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Cadeia de caracteres ou dados binários retornados para um parâmetro de saída resultaram em truncamento de caractere não vazios ou nulos de dados binários. Se fosse um valor de cadeia de caracteres, ele era truncados à direita. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|O valor de dados identificado pela *ValueType* argumento **SQLBindParameter** para o parâmetro associado não pôde ser convertido para o tipo de dados identificado pelo *ParameterType*argumento na **SQLBindParameter**.|  
|07S01|Uso inválido de parâmetro padrão|Um valor de parâmetro definido com **SQLBindParameter**, foi SQL_DEFAULT_PARAM, e o parâmetro correspondente não tem um valor padrão.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|22001|Dados de cadeia de caracteres, truncamento à direita|A atribuição de um caractere ou valor binário para uma coluna resultou em truncamento de não vazio (caractere) ou não nulo caracteres (binários) ou bytes.<br /><br /> O tipo de informação no SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "Y", e mais dados que foi enviados para um parâmetro longo (o tipo de dados era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específicos da fonte de dados longos) que foi especificado com o *StrLen_or_IndPtr* argumento **SQLBindParameter**.<br /><br /> O tipo de informação no SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "Y", e mais dados que foi enviados para uma coluna long (tipo de dados era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específicos da fonte de dados longos) que foi especificada no buffer de comprimento correspondente a uma coluna em uma linha de dados que foram adicionados ou atualizados com **SQLBulkOperations** ou foram atualizados com **SQLSetPos**.|  
|22003|Valor numérico fora do intervalo|Os dados enviados para um parâmetro numérico associado ou coluna fez parte inteira (em vez de fracionários) o número a ser truncado quando atribuído à coluna da tabela associada.<br /><br /> Retornar um valor numérico (como numérico ou cadeia de caracteres) para um ou mais parâmetros de entrada/saída ou de saída teria causado parte inteira (em vez de fracionários) o número a ser truncado.|  
|22007|Formato de data/hora inválido|Os dados enviados para uma coluna que foi associada a uma data, hora ou estrutura de carimbo de hora ou um parâmetro eram, respectivamente, uma data inválida, hora ou carimbo de hora.<br /><br /> Um parâmetro de entrada/saída ou de saída foi associado a uma data, hora ou estrutura de carimbo de hora C, e um valor no parâmetro retornado era, respectivamente, uma data inválida, hora ou carimbo de hora. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|22008|Estouro no campo de data e hora|Uma expressão de data e hora é calculado para uma entrada/saída ou parâmetro de saída resultou em uma data, hora ou estrutura de carimbo de hora C que era inválida.|  
|22012|Divisão por zero|Uma expressão aritmética é calculado para uma entrada/saída ou parâmetro de saída que resultou na divisão por zero.|  
|22015|Estouro no campo de intervalo|Os dados enviados para uma coluna numérica ou de intervalo exata ou parâmetro para um tipo de dados SQL intervalo causou uma perda de dígitos significativos.<br /><br /> Dados foi enviados para uma coluna de intervalo ou um parâmetro com mais de um campo, foi convertidos em um tipo de dados numéricos e não tinham nenhuma representação no tipo de dados numérico.<br /><br /> Os dados enviados para a coluna ou dados de parâmetro foi atribuídos a um intervalo de tipo de SQL e não havia nenhuma representação do valor do tipo C no intervalo de tipo SQL.<br /><br /> Os dados enviados para um numérico exato ou a coluna de intervalo de C ou o parâmetro para um tipo de intervalo C causou uma perda de dígitos significativos.<br /><br /> Os dados enviados para a coluna ou dados de parâmetro foi atribuídos a uma estrutura de intervalo de C e não havia nenhuma representação dos dados na estrutura de dados de intervalo.|  
|22018|Valor de caractere inválido para especificação de conversão|O tipo C era um valor numérico exato ou aproximado, uma data e hora ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna ou parâmetro não era um literal válido do tipo C associado.<br /><br /> O tipo de SQL era um valor numérico exato ou aproximado, uma data e hora ou um tipo de dados de intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna ou parâmetro não era um literal válido do tipo SQL associado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|(DM) o argumento *DataPtr* era um ponteiro nulo e o argumento *StrLen_or_Ind* não era 0, SQL_DEFAULT_PARAM ou SQL_NULL_DATA.|  
|HY010|Erro de sequência de função|(DM) a chamada de função anterior não era uma chamada para **SQLPutData** ou **SQLParamData**.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando a função SQLPutData foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY019|Dados não caracteres e não binários enviados em partes|**SQLPutData** foi chamado mais de uma vez para uma coluna ou parâmetro e não estava sendo usado para enviar dados de caractere C para uma coluna com um tipo específico de fonte de dados character, binary ou dados ou para enviar dados binários de C para uma coluna com um caractere , binário ou tipo de dados específicos da fonte de dados.|  
|HY020|Tentativa de concatenar um valor nulo|**SQLPutData** foi chamado mais de uma vez desde a chamada que retornado SQL_NEED_DATA e em uma dessas chamadas, o *StrLen_or_Ind* argumento contidos SQL_NULL_DATA ou SQL_DEFAULT_PARAM.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|O argumento *DataPtr* não era um ponteiro nulo e o argumento *StrLen_or_Ind* era menor que 0, mas não é igual a SQL_NTS ou SQL_NULL_DATA.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
 Se **SQLPutData** é chamado durante o envio de dados para um parâmetro em uma instrução SQL, ele pode retornar qualquer SQLSTATE que pode ser retornado pela função chamada para executar a instrução (**SQLExecute** ou **SQLExecDirect**). Se for chamado durante o envio de dados de uma coluna que está sendo atualizada ou adicionada com **SQLBulkOperations** ou que está sendo atualizada com **SQLSetPos**, ele pode retornar qualquer SQLSTATE que pode ser retornado por  **SQLBulkOperations** ou **SQLSetPos**.  
  
## <a name="comments"></a>Comentários  
 **SQLPutData** pode ser chamado para fornecer dados de dados em execução para dois usos: dados de parâmetro a serem usados em uma chamada para **SQLExecute** ou **SQLExecDirect**, ou dados da coluna a ser usado quando uma linha é atualizada ou adicionados por uma chamada para **SQLBulkOperations** ou é atualizada por uma chamada para **SQLSetPos**.  
  
 Quando um aplicativo chama **SQLParamData** para determinar quais dados devem enviar, o driver retorna um indicador de que o aplicativo pode usar para determinar quais dados de parâmetro para enviar ou onde os dados da coluna podem ser encontrados. Ele também retorna SQL_NEED_DATA, que é um indicador para o aplicativo que ele deverá chamar **SQLPutData** para enviar os dados. No *DataPtr* argumento **SQLPutData**, o aplicativo passa um ponteiro para o buffer que contém os dados reais para o parâmetro ou coluna.  
  
 Quando o driver retornará SQL_SUCCESS para **SQLPutData**, o aplicativo chama **SQLParamData** novamente. **SQLParamData** retornará SQL_NEED_DATA se precisam de mais dados a serem enviados, caso em que o aplicativo chama **SQLPutData** novamente. Ele retorna SQL_SUCCESS se tiver sido enviado a todos os dados de dados em execução. O aplicativo, em seguida, chama **SQLParamData** novamente. Se o driver retorna SQL_NEED_DATA e outro indicador no  *\*ValuePtrPtr*, ele requer dados para outro parâmetro ou coluna e **SQLPutData** é chamado novamente. Se o driver retornará SQL_SUCCESS, em seguida, todos os dados em execução os dados foram enviados e pode ser executada a instrução SQL ou o **SQLBulkOperations** ou **SQLSetPos** chamada pode ser processada.  
  
 Para obter mais informações sobre os dados de parâmetro como dados em execução são passadas em tempo de execução de instrução, consulte "Passando valores de parâmetro" na [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [enviando dados Long](../../../odbc/reference/develop-app/sending-long-data.md). Para obter mais informações sobre os dados da coluna como dados em execução são atualizadas ou adicionadas, consulte a seção "Usando SQLSetPos" em [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Executando em massa atualizações usando indicadores" no [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), e [Dados long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
> [!NOTE]  
>  Um aplicativo pode usar **SQLPutData** para enviar dados em partes somente ao enviar dados de caractere C para uma coluna com um tipo específico de fonte de dados character, binary ou dados ou ao enviar dados binários de C para uma coluna com um caractere, binária, ou dados tipo de dados de origem específicos. Se **SQLPutData** é chamado mais de uma vez em outras condições, ela retornará SQL_ERROR e SQLSTATE HY019 (não caracteres e não binários dados enviados em partes).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir pressupõe que um nome de fonte de dados chamado teste. O banco de dados associado deve ter uma tabela que você pode criar, da seguinte maneira:  
  
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
|Um buffer de associação a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornar o próximo parâmetro para enviar dados|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
