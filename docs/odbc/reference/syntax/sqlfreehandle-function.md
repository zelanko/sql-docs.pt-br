---
title: Função SQLFreeHandle | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b136dec98a19676aa67c78615d8fe931f62aafa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285767"
---
# <a name="sqlfreehandle-function"></a>Função SQLFreeHandle
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLFreeHandle** libera recursos associados a um ambiente específico, conexão, instrução ou alça de descritor.  
  
> [!NOTE]
>  Esta função é uma função genérica para liberar alças. Ele substitui as funções ODBC 2.0 **SQLFreeConnect** (para liberar uma alça de conexão) e **SQLFreeEnv** (para liberar uma alça de ambiente). **SQLFreeConnect** e **SQLFreeEnv** são ambos preteridos em ODBC 3 *.x*. **O SQLFreeHandle** também substitui a função ODBC 2.0 **SQLFreeStmt** (com a *opção*SQL_DROP) para liberar uma alça de declaração. Para obter mais informações, consulte "Comentários". Para obter mais informações sobre o que o Driver Manager mapeia essa função para quando um aplicativo ODBC 3 *.x* estiver trabalhando com um driver ODBC*2.x,* consulte [Funções de substituição de mapeamento para compatibilidade retrógrada de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Handletype*  
 [Entrada] O tipo de alça a ser liberada pelo **SQLFreeHandle**. Deve ser um dos seguintes valores:   
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN alça é usada apenas pelo Driver Manager e pelo motorista. Os aplicativos não devem usar este tipo de alça. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [Developing Connection-Pool Awareness em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 Se *handleType* não for um desses valores, **o SQLFreeHandle** retorna SQL_INVALID_HANDLE.  
  
 *Handle*  
 [Entrada] A alça para ser liberada.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
 Se **o SQLFreeHandle** retornar SQL_ERROR, a alça ainda será válida.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLFreeHandle** retorna SQL_ERROR, um valor SQLSTATE associado pode ser obtido a partir da estrutura de dados de diagnóstico para o cabo que o **SQLFreeHandle** tentou libertar, mas não conseguiu. A tabela a seguir lista os valores SQLSTATE normalmente retornados pelo **SQLFreeHandle** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) O argumento *HandleType* foi SQL_HANDLE_ENV, e pelo menos uma conexão estava em um estado alocado ou conectado. **SQLDisconnect** e **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DBC devem ser chamados para cada conexão antes de ligar para **o SQLFreeHandle** com um *HandleType* de SQL_HANDLE_ENV.<br /><br /> (DM) O argumento *HandleType* foi SQL_HANDLE_DBC, e a função foi chamada antes de chamar **SQLDisconnect** para a conexão.<br /><br /> (DM) O argumento *HandleType* foi SQL_HANDLE_DBC. Uma função de execução assíncrona foi chamada com *Handle* e a função ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) O argumento *HandleType* foi SQL_HANDLE_STMT. **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados com a alça da declaração e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) O argumento *HandleType* foi SQL_HANDLE_STMT. Uma função de execução assíncrona foi chamada no cabo da declaração ou no cabo de conexão associado e a função ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) O argumento *HandleType* foi SQL_HANDLE_DESC. Uma função de execução assíncrona foi chamada no cabo de conexão associado; e a função ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) Todas as alças subsidiárias e outros recursos não foram liberados antes **da chamada SQLFreeHandle.**<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foi chamado para que uma das alças de declaração associadas ao *Handle* and *HandleType* fosse definida como SQL_HANDLE_STMT ou SQL_HANDLE_DESC devolvida SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|O argumento *HandleType* foi SQL_HANDLE_STMT ou SQL_HANDLE_DESC, e a chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido a condições de memória baixas.|  
|HY017|Uso inválido de uma alça descritor alocada automaticamente.|(DM) O *argumento Handle* foi definido como o punho de um descritor alocado automaticamente.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O argumento *HandleType* foi SQL_HANDLE_DESC, e o motorista era um driver ODBC 2 *.x.*<br /><br /> (DM) O argumento *HandleType* foi SQL_HANDLE_STMT, e o motorista não era um driver ODBC válido.|  
  
## <a name="comments"></a>Comentários  
 **O SQLFreeHandle** é usado para liberar alças para ambientes, conexões, instruções e descritores, conforme descrito nas seções a seguir. Para obter informações gerais sobre alças, consulte [Handles](../../../odbc/reference/develop-app/handles.md).  
  
 Um aplicativo não deve usar uma alça depois de ser liberada; o Driver Manager não verifica a validade de uma alça em uma chamada de função.  
  
## <a name="freeing-an-environment-handle"></a>Liberando uma alça de ambiente  
 Antes de chamar **sQLFreeHandle** com um *HandleType* de SQL_HANDLE_ENV, um aplicativo deve chamar **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DBC para todas as conexões alocadas no ambiente. Caso contrário, a chamada para **SQLFreeHandle** retorna SQL_ERROR e o ambiente e qualquer conexão ativa permanece válida. Para obter mais informações, consulte [Environment Handles](../../../odbc/reference/develop-app/environment-handles.md) and [Alocaing the Environment Handle .](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)  
  
 Se o ambiente for um ambiente compartilhado, o aplicativo que chama **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_ENV não tiver mais acesso ao ambiente após a chamada, mas os recursos do ambiente não são necessariamente liberados. A chamada para **SQLFreeHandle** decreta a contagem de referência do ambiente. A contagem de referências é mantida pelo Driver Manager. Se não chegar a zero, o ambiente compartilhado não será liberado, pois ainda está sendo usado por outro componente. Se a contagem de referência chegar a zero, os recursos do ambiente compartilhado serão liberados.  
  
## <a name="freeing-a-connection-handle"></a>Liberando uma alça de conexão  
 Antes de chamar **sQLFreeHandle** com um *HandleType* de SQL_HANDLE_DBC, um aplicativo deve chamar **SQLDisconnect** para a conexão se houver uma conexão nesta alça *.* Caso contrário, a chamada para **SQLFreeHandle** retorna SQL_ERROR e a conexão permanece válida.  
  
 Para obter mais informações, consulte ['Alças de conexão'](../../../odbc/reference/develop-app/connection-handles.md) e [desconexão de uma fonte de dados ou driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="freeing-a-statement-handle"></a>Liberando um identificador de instrução  
 Uma chamada para **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_STMT libera todos os recursos que foram alocados por uma chamada para **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_STMT. Quando um aplicativo chama **o SQLFreeHandle** para liberar uma declaração que tem resultados pendentes, os resultados pendentes são excluídos. Quando um aplicativo libera uma alça de declaração, o motorista libera os quatro descritores alocados automaticamente associados a essa alça. Para obter mais informações, consulte ['Alças de declaração'](../../../odbc/reference/develop-app/statement-handles.md) e [a liberação de uma alça de declaração .](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)  
  
 Observe que **o SQLDisconnect** descarta automaticamente quaisquer instruções e descritores abertos na conexão.  
  
## <a name="freeing-a-descriptor-handle"></a>Liberando uma alça do descritor  
 Uma chamada para **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DESC libera a alça do descritor em *Handle*. A chamada para **SQLFreeHandle** não libera nenhuma memória alocada pelo aplicativo que possa ser referenciada por um campo de ponteiro (incluindo SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR) de qualquer registro descritor de *Handle*. A memória alocada pelo driver para campos que não são campos de ponteiro é liberada quando a alça é liberada. Quando uma alça de descritor alocada pelo usuário é liberada, todas as declarações com as que a alça liberada foram associadas revertem para suas respectivas alças de descritor automaticamente alocadas.  
  
> [!NOTE]
>  Os drivers ODBC*2.x* não suportam alças de descritores de liberação, assim como não suportam a alocação de alças descritores.  
  
 Observe que **o SQLDisconnect** descarta automaticamente quaisquer instruções e descritores abertos na conexão. Quando um aplicativo libera uma alça de declaração, o motorista libera todos os descritores gerados automaticamente associados a essa alça.  
  
 Para obter mais informações sobre descritores, consulte [Descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Para obter amostras adicionais de código, consulte [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) e [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
### <a name="code"></a>Código  
  
```cpp  
// SQLFreeHandle.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <stdio.h>  
  
int main() {  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   // Initialize the environment, connection, statement handles.  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   // Allocate the environment.  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set environment attributes.  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
  
   // Allocate the connection.  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
   // Set the login timeout.  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
  
   // Let the user select the data source and connect to the database.  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Free handles, and disconnect.     
   if (hstmt) {   
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
      hstmt = NULL;   
   }  
   if (hdbc) {   
      SQLDisconnect(hdbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      hdbc = NULL;   
   }  
   if (henv) {   
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
      henv = NULL;   
   }  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando uma alça|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Cancelamento do processamento de declarações|[Funl SQLCance](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Definindo um nome do cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md)
