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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e252769c26a5491100094b1243b9c2c6bb67d94d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285696"
---
# <a name="sqlfreestmt-function"></a>Função SQLFreeStmt
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLFreeStmt** deixa de processar associado a uma instrução específica, fecha todos os cursores abertos associados à instrução, descarta resultados pendentes ou, opcionalmente, libera todos os recursos associados à alça da declaração.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração  
  
 *Opção*  
 [Entrada] Uma das seguintes opções:  
  
 SQL_ CLOSE: Fecha o cursor associado ao *StatementHandle* (se um foi definido) e descarta todos os resultados pendentes. O aplicativo pode reabrir este cursor mais tarde executando uma declaração **SELECT** novamente com os mesmos ou diferentes valores de parâmetro. Se nenhum cursor estiver aberto, esta opção não tem efeito para a aplicação. **SQLCloseCursor** também pode ser chamado para fechar um cursor. Para obter mais informações, consulte [Fechando o Cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 SQL_DROP: Esta opção é preterida. Uma chamada para **SQLFreeStmt** com uma *opção* de SQL_DROP é mapeada no Driver Manager para [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
 SQL_UNBIND: Define o campo SQL_DESC_COUNT do ARD para 0, liberando todos os buffers de coluna vinculados pelo **SQLBindCol** para o *deditoHandle*dado . Isso não desvincula a coluna de marcadores; para fazer isso, o campo SQL_DESC_DATA_PTR do ARD para a coluna marcador é definido como NULL. Observe que se esta operação for realizada em um descritor explicitamente alocado que é compartilhado por mais de uma declaração, a operação afetará as vinculações de todas as declarações que compartilham o descritor. Para obter mais informações, consulte [Visão geral dos resultados de recuperação (básico)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 SQL_RESET_PARAMS: Define o campo SQL_DESC_COUNT da APD como 0, liberando todos os buffers de parâmetro sdefinidos pelo **SQLBindParameter** para a determinada *StatementHandle*. Se esta operação for realizada em um descritor explicitamente alocado que é compartilhado por mais de uma declaração, esta operação afetará as vinculações de todas as declarações que compartilham o descritor. Para obter mais informações, consulte [Parâmetros de vinculação](../../../odbc/reference/develop-app/binding-parameters-odbc.md).  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLFreeStmt** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementhandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLFreeStmt** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando **SQLFreeStmt** foi chamado.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada com *opção* definida para SQL_RESET_PARAMS antes que os dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY092|Tipo de opção fora do alcance|(DM) O valor especificado para a *opção* de argumento não era:<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Chamar **o SQLFreeStmt** com a opção SQL_CLOSE é equivalente a chamar **sqlCloseCursor**, exceto que **o SQLFreeStmt** com SQL_CLOSE não afeta o aplicativo se nenhum cursor estiver aberto na declaração. Se nenhum cursor estiver aberto, uma chamada para **SQLCloseCursor** retorna SQLSTATE 24000 (estado de cursor inválido).  
  
 Um aplicativo não deve usar uma alça de declaração depois de ser liberada; o Driver Manager não verifica a validade de uma alça em uma chamada de função.  
  
## <a name="example"></a>Exemplo  
 É uma boa prática de programação para alças livres. No entanto, para simplificar, a amostra a seguir não inclui código que libera alças alocadas. Para obter um exemplo de como liberar as alças, consulte [SQLFreeHandle Function](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
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
|Alocando uma alça|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Fechando um cursor|[Função SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Liberando uma alça|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Definindo um nome do cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
