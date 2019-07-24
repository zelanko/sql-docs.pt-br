---
title: Função SQLDisconnect | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 788ca2eb7cf37314eb7d5386a23f17123f9ccaff
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343012"
---
# <a name="sqldisconnect-function"></a>Função SQLDisconnect
**Conformidade**  
 Versão introduzida: Conformidade com os padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLDisconnect** fecha a conexão associada a um identificador de conexão específico.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexão.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLDisconnect** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e um *identificador* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados  por SQLDisconnect e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01002|Erro de desconexão|Ocorreu um erro durante a desconexão. No entanto, a desconexão foi bem-sucedida. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) a conexão especificada no argumento *ConnectionHandle* não foi aberta.|  
|25000|Estado de transação inválido|Houve uma transação em andamento na conexão especificada pelo argumento *ConnectionHandle*. A transação permanece ativa.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no  *\*buffer MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A função foi chamada e, antes de terminou a execução da [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) , foi chamada no *ConnectionHandle*. Em seguida, a função foi chamada novamente no *ConnectionHandle*.<br /><br /> A função foi chamada e antes de concluir a execução de **SQLCancelHandle** foi chamada no *ConnectionHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para um *StatementHandle* associado ao *ConnectionHandle* e ainda estava em execução quando SQLDisconnect foi chamado.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *ConnectionHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para um *StatementHandle* associado ao *ConnectionHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação e a conexão ainda esteja ativa. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *ConnectionHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Se um aplicativo chamar **SQLDisconnect** após **SQLBrowseConnect** retornar SQL_NEED_DATA e antes de retornar um código de retorno diferente, o driver cancelará o processo de navegação de conexão e retornará a conexão a um estado não conectado.  
  
 Se um aplicativo chamar **SQLDisconnect** enquanto houver uma transação incompleta associada ao identificador de conexão, o driver retornará SQLSTATE 25000 (estado de transação inválido), indicando que a transação está inalterada e a conexão será abrir. Uma transação incompleta é aquela que não foi confirmada ou revertida com **SQLEndTran**.  
  
 Se um aplicativo chamar **SQLDisconnect** antes de liberar todas as instruções associadas à conexão, o driver, após a desconexão com êxito da fonte de dados, liberará essas instruções e todos os descritores que foram explicitamente alocados na conexão. No entanto, se uma ou mais das instruções associadas à conexão ainda estiverem sendo executadas de  forma assíncrona, SQLDisconnect retornará SQL_ERROR com um valor SQLSTATE de HY010 (erro de sequência de função). Além disso  , SQLDisconnect liberará todas as instruções associadas e todos os descritores que foram explicitamente alocados na conexão, se a conexão estiver em um estado suspenso ou se SQLDisconnect tiver sido cancelado com êxito por   **SQLCancelHandle**.  
  
 Para obter informações sobre como um aplicativo usa SQLDisconnect, consulte desconectando [de uma fonte de dados ou driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="disconnecting-from-a-pooled-connection"></a>Desconectando de uma conexão em pool  
 Se o pool de conexões estiver habilitado para um ambiente compartilhado e um aplicativo  chamar SQLDisconnect em uma conexão nesse ambiente, a conexão será retornada ao pool de conexões e ainda estará disponível para outros componentes usando o mesmo compartilhamento compartilhado ambiente.  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [exemplo de programa de ODBC](../../../odbc/reference/sample-odbc-program.md), [função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)e [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Conectando-se a uma fonte de dados usando uma cadeia de conexão ou caixa de diálogo|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Executando uma operação Commit ou ROLLBACK|[Função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Liberando um identificador de conexão|[Função SQLFreeConnect](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
