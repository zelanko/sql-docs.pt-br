---
title: Função SQLFreeHandle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f63af414d59afed2bbe2e8eed3fba7a1362bb4bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061466"
---
# <a name="sqlfreehandle-function"></a>Função SQLFreeHandle
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLFreeHandle** libera recursos associados a um identificador de ambiente, conexão, instrução ou descritor específico.  
  
> [!NOTE]
>  Essa função é uma função genérica para liberar identificadores. Ele substitui as funções ODBC 2.0 **SQLFreeConnect** (para liberar um identificador de conexão) e **SQLFreeEnv** (para liberar um identificador de ambiente). **SQLFreeConnect** e **SQLFreeEnv** foram preteridos em ODBC 3 *. x*. **SQLFreeHandle** também substitui a função ODBC 2.0 **SQLFreeStmt** (com o SQL_DROP *opção*) para liberar um identificador de instrução. Para obter mais informações, consulte "Comentários". Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 3 *. x* aplicativo está funcionando com um ODBC 2 *. x* driver, consulte [funções de mapeamento de substituição para trás Compatibilidade de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] O tipo de identificador a ser liberada por **SQLFreeHandle**. Deve ser um dos seguintes valores:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Identificador SQL_HANDLE_DBC_INFO_TOKEN é usado somente pelo Gerenciador de Driver e o driver. Aplicativos não devem usar esse tipo de identificador. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento de Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 Se *HandleType* não é um destes valores **SQLFreeHandle** retorne SQL_INVALID_HANDLE.  
  
 *Handle*  
 [Entrada] O identificador a ser liberado.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
 Se **SQLFreeHandle** retorna SQL_ERROR, o identificador ainda é válido.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLFreeHandle** retorna SQL_ERROR, um valor SQLSTATE associado pode ser obtida da estrutura de dados de diagnóstico para o identificador que **SQLFreeHandle** tentou gratuito, mas não foi possível. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLFreeHandle** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) a *HandleType* argumento era SQL_HANDLE_ENV e pelo menos uma conexão estava em um estado conectado ou alocado. **SQLDisconnect** e **SQLFreeHandle** com um *HandleType* SQL_HANDLE_DBC deve ser chamado para cada conexão antes de chamar **SQLFreeHandle** com um *HandleType* SQL_HANDLE_ENV.<br /><br /> (DM) a *HandleType* argumento era SQL_HANDLE_DBC e a função foi chamada antes de chamar **SQLDisconnect** para a conexão.<br /><br /> (DM) a *HandleType* argumento era SQL_HANDLE_DBC. Uma função de execução assíncrona foi chamada com *manipular* e a função ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) a *HandleType* argumento era SQL_HANDLE_STMT. **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado com o identificador de instrução e retornou SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) a *HandleType* argumento era SQL_HANDLE_STMT. Uma função de execução assíncrona foi chamada no identificador da instrução ou o identificador de conexão associado e a função ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) a *HandleType* argumento era SQL_HANDLE_DESC. Uma função de execução assíncrona foi chamada no identificador de conexão associado; e a função ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) identificadores de todas as subsidiárias e outros recursos não foram lançados antes **SQLFreeHandle** foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para uma das alças de instrução associadas com o *manipular* e *HandleType* foi definido como SQL_HANDLE_STMT ou SQL_HANDLE_DESC retornado SQL_PARAM_DATA_AVAILABLE. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|O *HandleType* argumento era SQL_HANDLE_STMT ou SQL_HANDLE_DESC, e a chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY017|Uso inválido de um identificador do descritor alocado automaticamente.|(DM) a *manipular* argumento foi definido como o identificador para um descritor alocado automaticamente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|(DM) a *HandleType* argumento era SQL_HANDLE_DESC, e o driver foi um ODBC 2 *. x* driver.<br /><br /> (DM) a *HandleType* argumento era SQL_HANDLE_STMT e o driver não era um driver ODBC válido.|  
  
## <a name="comments"></a>Comentários  
 **SQLFreeHandle** é usado para liberar identificadores de ambientes, conexões, instruções e descritores, conforme descrito nas seções a seguir. Para obter informações gerais sobre identificadores, consulte [identificadores](../../../odbc/reference/develop-app/handles.md).  
  
 Um aplicativo não deve usar um identificador depois de ele ter sido liberado; o Gerenciador de Driver não verifica a validade de um identificador de uma chamada de função.  
  
## <a name="freeing-an-environment-handle"></a>Liberando um identificador de ambiente  
 Antes de chamar **SQLFreeHandle** com um *HandleType* SQL_HANDLE_ENV, um aplicativo deve chamar **SQLFreeHandle** com um *HandleType*SQL_HANDLE_DBC para todas as conexões alocada sob o ambiente. Caso contrário, a chamada para **SQLFreeHandle** retorna SQL_ERROR e o ambiente e qualquer conexão ativa permanece válido. Para obter mais informações, consulte [ambiente manipula](../../../odbc/reference/develop-app/environment-handles.md) e [alocar o identificador de ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Se o ambiente é um ambiente compartilhado, o aplicativo que chama **SQLFreeHandle** com um *HandleType* SQL_HANDLE_ENV não tem mais acesso para o ambiente após a chamada, mas o ambiente recursos não são necessariamente liberados. A chamada para **SQLFreeHandle** diminui a contagem de referência do ambiente. A contagem de referência é mantida pelo Gerenciador de Driver. Se ele não atinja zero, o ambiente compartilhado não é liberado, porque ainda está sendo usado por outro componente. Se a contagem de referência chegar a zero, os recursos do ambiente compartilhado são liberados.  
  
## <a name="freeing-a-connection-handle"></a>Liberando um identificador de Conexão  
 Antes de chamar **SQLFreeHandle** com um *HandleType* SQL_HANDLE_DBC, um aplicativo deve chamar **SQLDisconnect** para a conexão se não houver uma conexão sobre isso lidar com *.* Caso contrário, a chamada para **SQLFreeHandle** retorna SQL_ERROR e a conexão permanece válido.  
  
 Para obter mais informações, consulte [Conexão manipula](../../../odbc/reference/develop-app/connection-handles.md) e [desconectar-se de uma fonte de dados ou Driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="freeing-a-statement-handle"></a>Liberando um identificador de instrução  
 Uma chamada para **SQLFreeHandle** com um *HandleType* sql_handle_stmt libera todos os recursos que foram alocados por uma chamada a **SQLAllocHandle** com um  *HandleType* sql_handle_stmt. Quando um aplicativo chama **SQLFreeHandle** para liberar uma instrução com resultados pendentes, os resultados pendentes serão excluídos. Quando um aplicativo libera um identificador de instrução, o driver libera os descritores de alocado automaticamente quatro associados com esse identificador. Para obter mais informações, consulte [instrução trata](../../../odbc/reference/develop-app/statement-handles.md) e [liberando um identificador de instrução](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 Observe que **SQLDisconnect** descarta automaticamente quaisquer instruções e descritores de abrir a conexão.  
  
## <a name="freeing-a-descriptor-handle"></a>Liberando um identificador do descritor  
 Uma chamada para **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DESC libera o identificador do descritor na *manipular*. A chamada para **SQLFreeHandle** não libere toda a memória alocada pelo aplicativo que pode ser referenciado por um campo de ponteiro (incluindo SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR) de qualquer registro do descritor de *manipular*. A memória alocada pelo driver para os campos que não são campos de ponteiro é liberada quando o identificador é liberado. Quando um identificador do descritor alocado pelo usuário é liberado, todas as instruções que a alça liberada tinha sido associada com revertem para os identificadores de descritor alocado automaticamente respectivo.  
  
> [!NOTE]
>  2 de ODBC *. x* drivers não dão suporte a identificadores de descritor liberando, assim que eles não dão suporte ao alocar identificadores de descritor.  
  
 Observe que **SQLDisconnect** descarta automaticamente quaisquer instruções e descritores de abrir a conexão. Quando um aplicativo libera um identificador de instrução, o driver libera todos os descritores de gerado automaticamente associados com esse identificador.  
  
 Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Para obter exemplos de código adicionais, consulte [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) e [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
### <a name="code"></a>Código  
  
```  
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
|Cancelando o processamento de instrução|[SQLCance Functionl](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Configuração de um nome de cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md)
