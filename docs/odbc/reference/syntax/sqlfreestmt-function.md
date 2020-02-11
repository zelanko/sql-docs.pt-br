---
title: Função SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6141f3efe357bfb3f14c04aa2f6760e9470649a6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68345151"
---
# <a name="sqlfreestmt-function"></a>Função SQLFreeStmt
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLFreeStmt** interrompe o processamento associado a uma instrução específica, fecha os cursores abertos associados à instrução, descarta os resultados pendentes ou, opcionalmente, libera todos os recursos associados ao identificador da instrução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução  
  
 *Opção*  
 Entrada Uma das seguintes opções:  
  
 SQL_ fechar: fecha o cursor associado a *StatementHandle* (se um tiver sido definido) e descarta todos os resultados pendentes. O aplicativo pode reabrir esse cursor posteriormente executando uma instrução **Select** novamente com os mesmos valores de parâmetro ou diferentes. Se nenhum cursor estiver aberto, essa opção não terá nenhum efeito para o aplicativo. **SQLCloseCursor** também pode ser chamado para fechar um cursor. Para obter mais informações, consulte [fechando o cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 SQL_DROP: essa opção é preterida. Uma chamada para **SQLFreeStmt** com uma *opção* de SQL_DROP é mapeada no Gerenciador de driver para [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
 SQL_UNBIND: define o campo SQL_DESC_COUNT de ARD como 0, liberando todos os buffers de coluna associados por **SQLBindCol** para o *StatementHandle*determinado. Isso não desassocia a coluna de indicadores; para fazer isso, o campo SQL_DESC_DATA_PTR do ARD para a coluna Bookmark é definido como NULL. Observe que, se essa operação for executada em um descritor explicitamente alocado que é compartilhado por mais de uma instrução, a operação afetará as associações de todas as instruções que compartilham o descritor. Para obter mais informações, consulte [visão geral da recuperação de resultados (básico)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 SQL_RESET_PARAMS: define o campo SQL_DESC_COUNT do APD como 0, liberando todos os buffers de parâmetro definidos por **SQLBindParameter** para o *StatementHandle*determinado. Se essa operação for executada em um descritor explicitamente alocado que é compartilhado por mais de uma instrução, essa operação afetará as associações de todas as instruções que compartilham o descritor. Para obter mais informações, consulte [parâmetros de associação](../../../odbc/reference/develop-app/binding-parameters-odbc.md).  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLFreeStmt** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLFreeStmt** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando **SQLFreeStmt** foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Essa função foi chamada com a *opção* definida como SQL_RESET_PARAMS antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY092|Tipo de opção fora do intervalo|(DM) o valor especificado para a *opção* de argumento não era:<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Chamar **SQLFreeStmt** com a opção SQL_CLOSE é equivalente a chamar **SQLCloseCursor**, exceto que **SQLFreeStmt** com SQL_CLOSE não afeta o aplicativo se nenhum cursor estiver aberto na instrução. Se nenhum cursor estiver aberto, uma chamada para **SQLCloseCursor** retornará SQLSTATE 24000 (estado de cursor inválido).  
  
 Um aplicativo não deve usar um identificador de instrução depois que ele foi liberado; o Gerenciador de driver não verifica a validade de um identificador em uma chamada de função.  
  
## <a name="example"></a>Exemplo  
 É uma boa prática de programação para liberar identificadores. No entanto, para simplificar, o exemplo a seguir não inclui um código que libera identificadores alocados. Para obter um exemplo de como liberar identificadores, consulte a [função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
```cpp  
// SQLFreeStmt.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
   retCode = SQLFreeStmt(hstmt, SQL_UNBIND);  
   retCode = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Fechando um cursor|[Função SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Liberando um identificador|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Definindo um nome de cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
