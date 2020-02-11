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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e312bcbc6efcb96ff02657b98034f0340ae377dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68345179"
---
# <a name="sqlfreehandle-function"></a>Função SQLFreeHandle
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 O **SQLFreeHandle** libera recursos associados a um ambiente, uma conexão, uma instrução ou um identificador de descritor específico.  
  
> [!NOTE]
>  Essa função é uma função genérica para a liberação de identificadores. Ele substitui as funções de ODBC 2,0 **SQLFreeConnect** (para liberar um identificador de conexão) e **SQLFreeEnv** (para liberar um identificador de ambiente). **SQLFreeConnect** e **SQLFreeEnv** são preteridos no ODBC 3 *. x*. O **SQLFreeHandle** também substitui a função **SQLFreeStmt** do ODBC 2,0 (com a *opção*SQL_DROP) para liberar um identificador de instrução. Para obter mais informações, consulte "Comentários". Para obter mais informações sobre como o Gerenciador de driver mapeia essa função quando um aplicativo ODBC 3 *. x* está trabalhando com um driver ODBC 2 *. x* , consulte [mapeando funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 Entrada O tipo de identificador a ser liberado por **SQLFreeHandle**. Deve ser um dos seguintes valores:   
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 O identificador de SQL_HANDLE_DBC_INFO_TOKEN é usado somente pelo driver e pelo Gerenciador de driver. Os aplicativos não devem usar esse tipo de identificador. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento do pool de conexões em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 Se *HandleType* não for um desses valores, **SQLFreeHandle** retornará SQL_INVALID_HANDLE.  
  
 *Handle*  
 Entrada O identificador a ser liberado.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
 Se **SQLFreeHandle** retornar SQL_ERROR, o identificador ainda será válido.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLFreeHandle** retorna SQL_ERROR, um valor SQLSTATE associado pode ser obtido na estrutura de dados de diagnóstico para o identificador que o **SQLFreeHandle** tentou liberar, mas não pôde fazê-lo. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLFreeHandle** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) o argumento *HandleType* foi SQL_HANDLE_ENV e pelo menos uma conexão estava em um estado alocado ou conectado. **SQLDisconnect** e **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DBC deve ser chamado para cada conexão antes de chamar **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_ENV.<br /><br /> (DM) o argumento *HandleType* foi SQL_HANDLE_DBC e a função foi chamada antes de chamar **SQLDisconnect** para a conexão.<br /><br /> (DM) o argumento *HandleType* foi SQL_HANDLE_DBC. Uma função de execução assíncrona foi chamada com *identificador* e a função ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) o argumento *HandleType* foi SQL_HANDLE_STMT. **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado com o identificador de instrução e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) o argumento *HandleType* foi SQL_HANDLE_STMT. Uma função de execução assíncrona foi chamada no identificador de instrução ou no identificador de conexão associado e a função ainda estava sendo executada quando essa função foi chamada.<br /><br /> (DM) o argumento *HandleType* foi SQL_HANDLE_DESC. Uma função de execução assíncrona foi chamada no identificador de conexão associado; e a função ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) todos os identificadores de subsidiárias e outros recursos não foram liberados antes de o **SQLFreeHandle** ser chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para um dos identificadores de instrução associados ao *identificador* e ao *handletype* definido como SQL_HANDLE_STMT ou SQL_HANDLE_DESC retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|O argumento *HandleType* foi SQL_HANDLE_STMT ou SQL_HANDLE_DESC, e a chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY017|Uso inválido de um identificador de descritor alocado automaticamente.|(DM) o argumento *Handle* foi definido como o identificador para um descritor alocado automaticamente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o argumento *HandleType* foi SQL_HANDLE_DESC e o driver era um driver ODBC 2 *. x* .<br /><br /> (DM) o argumento *HandleType* foi SQL_HANDLE_STMT e o driver não era um driver ODBC válido.|  
  
## <a name="comments"></a>Comentários  
 O **SQLFreeHandle** é usado para liberar identificadores para ambientes, conexões, instruções e descritores, conforme descritos nas seções a seguir. Para obter informações gerais sobre identificadores, consulte [Handles](../../../odbc/reference/develop-app/handles.md).  
  
 Um aplicativo não deve usar um identificador depois que ele foi liberado; o Gerenciador de driver não verifica a validade de um identificador em uma chamada de função.  
  
## <a name="freeing-an-environment-handle"></a>Liberando um identificador de ambiente  
 Antes de chamar **SQLFreeHandle** com um *handletype* de SQL_HANDLE_ENV, um aplicativo deve chamar **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DBC para todas as conexões alocadas no ambiente. Caso contrário, a chamada para **SQLFreeHandle** retornará SQL_ERROR e o ambiente e qualquer conexão ativa permanecerá válida. Para obter mais informações, consulte os [identificadores de ambiente](../../../odbc/reference/develop-app/environment-handles.md) e [a alocação do identificador de ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Se o ambiente for um ambiente compartilhado, o aplicativo que chama **SQLFreeHandle** com um *handletype* de SQL_HANDLE_ENV não terá mais acesso ao ambiente após a chamada, mas os recursos do ambiente não serão necessariamente liberados. A chamada para **SQLFreeHandle** decrementa a contagem de referência do ambiente. A contagem de referência é mantida pelo Gerenciador de driver. Se não chegar a zero, o ambiente compartilhado não será liberado, pois ele ainda está sendo usado por outro componente. Se a contagem de referência chegar a zero, os recursos do ambiente compartilhado serão liberados.  
  
## <a name="freeing-a-connection-handle"></a>Liberando um identificador de conexão  
 Antes de chamar **SQLFreeHandle** com um *handletype* de SQL_HANDLE_DBC, um aplicativo deverá chamar **SQLDisconnect** para a conexão se houver uma conexão nesse identificador *.* Caso contrário, a chamada para **SQLFreeHandle** retornará SQL_ERROR e a conexão permanecerá válida.  
  
 Para obter mais informações, consulte [identificadores de conexão](../../../odbc/reference/develop-app/connection-handles.md) e [desconexão de uma fonte de dados ou driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="freeing-a-statement-handle"></a>Liberando um identificador de instrução  
 Uma chamada para **SQLFreeHandle** com um *handletype* de SQL_HANDLE_STMT libera todos os recursos que foram alocados por uma chamada para **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_STMT. Quando um aplicativo chama **SQLFreeHandle** para liberar uma instrução com resultados pendentes, os resultados pendentes são excluídos. Quando um aplicativo libera um identificador de instrução, o driver libera os quatro descritores alocados automaticamente associados a esse identificador. Para obter mais informações, consulte manipuladores de [instruções](../../../odbc/reference/develop-app/statement-handles.md) e [liberando um identificador de instrução](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 Observe que **SQLDisconnect** descarta automaticamente quaisquer instruções e descritores abertos na conexão.  
  
## <a name="freeing-a-descriptor-handle"></a>Liberando um identificador de descritor  
 Uma chamada para **SQLFreeHandle** com um *handletype* de SQL_HANDLE_DESC libera o identificador do descritor no *identificador*. A chamada para **SQLFreeHandle** não libera nenhuma memória alocada pelo aplicativo que pode ser referenciada por um campo de ponteiro (incluindo SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR) de qualquer registro de descritor de *identificador*. A memória alocada pelo driver para campos que não são campos de ponteiro é liberada quando o identificador é liberado. Quando um identificador de descritor alocado pelo usuário é liberado, todas as instruções que o identificador liberado tinha sido associado à reversão para seus respectivos identificadores de descritor alocados automaticamente.  
  
> [!NOTE]
>  Os drivers ODBC 2 *. x* não dão suporte a identificadores de descritor de liberação, assim como não oferecem suporte a identificadores de descritor de alocação.  
  
 Observe que **SQLDisconnect** descarta automaticamente quaisquer instruções e descritores abertos na conexão. Quando um aplicativo libera um identificador de instrução, o driver libera todos os descritores gerados automaticamente associados a esse identificador.  
  
 Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Para obter exemplos de código adicionais, consulte [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) e [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
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
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Definindo um nome de cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md)
