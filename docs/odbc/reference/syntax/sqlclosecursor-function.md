---
description: Função SQLCloseCursor
title: Função SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCloseCursor
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCloseCursor
helpviewer_keywords:
- SQLCloseCursor function [ODBC]
ms.assetid: 05b0a054-e28d-4e16-b5b0-07418486b372
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b4abc6076d976640325475594b80d6d503b50fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448824"
---
# <a name="sqlclosecursor-function"></a>Função SQLCloseCursor
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLCloseCursor** fecha um cursor que foi aberto em uma instrução e descarta os resultados pendentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLCloseCursor(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLCloseCursor** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLCloseCursor** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|24.000|Estado de cursor inválido|Nenhum cursor foi aberto no *StatementHandle*. (Isso é retornado somente por um ODBC 3. Driver *x* .)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão associado ao *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 **SQLCloseCursor** retorna SQLSTATE 24000 (estado de cursor inválido) se nenhum cursor estiver aberto. Chamar **SQLCloseCursor** é equivalente a chamar **SQLFreeStmt** com a opção SQL_CLOSE, com a exceção de que **SQLFreeStmt** com SQL_CLOSE não terá efeito sobre o aplicativo se nenhum cursor estiver aberto na instrução, enquanto **SQLCloseCursor** retorna SQLSTATE 24000 (estado de cursor inválido).  
  
> [!NOTE]  
>  Se um ODBC 3. *x* aplicativo trabalhando com um ODBC 2. o driver *x* chama **SQLCloseCursor** quando nenhum cursor está aberto, SQLSTATE 24000 (estado de cursor inválido) não é retornado, pois o Gerenciador de driver mapeia **SQLCloseCursor** para **SQLFreeStmt** com SQL_CLOSE.  
  
 Para obter mais informações, consulte [fechando o cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte a função [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) e a [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Liberando um identificador|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Processando vários conjuntos de resultados|[Função SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
