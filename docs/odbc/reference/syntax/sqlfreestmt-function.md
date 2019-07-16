---
title: Função SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 83e62430e55a82c904e6cae996538225ac8282b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006223"
---
# <a name="sqlfreestmt-function"></a>Função SQLFreeStmt
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLFreeStmt** interrompe o processamento associado a uma instrução específica, fechará quaisquer cursores abertos associados à instrução, descartes resultados pendentes ou, opcionalmente, libera todos os recursos associados com o identificador de instrução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução  
  
 *Opção*  
 [Entrada] Uma das seguintes opções:  
  
 SQL _ FECHAR: Fecha o cursor associado *StatementHandle* (se estiver definido) e descarta todos os resultados pendentes. O aplicativo pode reabrir esse cursor posteriormente, executando uma **selecionar** instrução novamente com os valores de parâmetro iguais ou diferentes. Se nenhum cursor está aberto, essa opção não terá efeito para o aplicativo. **SQLCloseCursor** também pode ser chamado para fechar um cursor. Para obter mais informações, consulte [fechando o Cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 SQL_DROP: Essa opção foi preterida. Uma chamada para **SQLFreeStmt** com um *opção* de SQL_DROP é mapeado no Gerenciador de Driver para [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
 SQL_UNBIND: Define o campo SQL_DESC_COUNT da descartar a 0, liberando todos os buffers de coluna associado pelo **SQLBindCol** para o determinado *StatementHandle*. Isso não desassociar a coluna de indicador; Para fazer isso, o campo SQL_DESC_DATA_PTR de descartar o para a coluna de indicador é definido como NULL. Observe que, se essa operação é executada em um descritor alocado explicitamente que é compartilhado por mais de uma instrução, a operação afetará as associações de todas as instruções que compartilham o descritor. Para obter mais informações, consulte [visão geral de recuperando resultados (básico)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 SQL_RESET_PARAMS: Define o campo SQL_DESC_COUNT APD como 0, liberando todos os buffers de parâmetro definidos pelo **SQLBindParameter** para o determinado *StatementHandle*. Se essa operação é executada em um descritor alocado explicitamente que é compartilhado por mais de uma instrução, essa operação afetará as associações de todas as instruções que compartilham o descritor. Para obter mais informações, consulte [parâmetros de associação](../../../odbc/reference/develop-app/binding-parameters-odbc.md).  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLFreeStmt** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLFreeStmt** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando **SQLFreeStmt** foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada com *opção* definido como SQL_RESET_PARAMS antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY092|Tipo de opção fora do intervalo|(DM) o valor especificado para o argumento *opção* não era:<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Chamando **SQLFreeStmt** com o SQL_CLOSE opção é equivalente a chamar **SQLCloseCursor**, exceto pelo fato **SQLFreeStmt** SQL_CLOSE não afeta o aplicativo Se nenhum cursor é aberto na instrução. Se nenhum cursor é aberto, uma chamada para **SQLCloseCursor** retornará SQLSTATE 24000 (estado de cursor inválido).  
  
 Um aplicativo não deve usar um identificador de instrução depois de ele ter sido liberado; o Gerenciador de Driver não verifica a validade de um identificador de uma chamada de função.  
  
## <a name="example"></a>Exemplo  
 É uma boa prática de programação para liberar identificadores. No entanto, para simplificar, o exemplo a seguir não inclui código que libera alocado identificadores. Para obter um exemplo de como liberar identificadores, consulte [função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
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
|Fechar um cursor|[Função SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Liberando um identificador|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Configuração de um nome de cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
