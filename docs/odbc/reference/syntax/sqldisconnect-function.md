---
title: Função SQLDisconnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d211fff7cdc008988dd9f984e64838c8903c6dc9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813944"
---
# <a name="sqldisconnect-function"></a>Função SQLDisconnect
**Conformidade com**  
 Versão introduziu: Conformidade de padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLDisconnect** fecha a conexão associada com um identificador de conexão específica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Identificador da conexão*  
 [Entrada] Identificador de Conexão.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLDisconnect** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_DBC e uma *manipular* dos *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDisconnect** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01002|Erro de desconexão|Ocorreu um erro durante a desconexão. No entanto, a desconexão foi bem-sucedida. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) a conexão especificada no argumento *ConnectionHandle* não foi aberta.|  
|25000|Estado de transação inválido|Houve uma transação em processo em que a conexão especificada pelo argumento *ConnectionHandle*. A transação permanecerá ativa.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A função foi chamada, e antes que ele terminou de executar [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamado na *ConnectionHandle*. Em seguida, a função foi chamada novamente na *ConnectionHandle*.<br /><br /> A função foi chamada e antes ele terminou de ser executada **SQLCancelHandle** foi chamado na *ConnectionHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para um *StatementHandle* associado com o *ConnectionHandle* e ainda estava em execução quando **SQLDisconnect** foi chamado.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *ConnectionHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para um *StatementHandle*  associado com o *ConnectionHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação e a conexão ainda está ativa. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *ConnectionHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Se um aplicativo chamar **SQLDisconnect** após **SQLBrowseConnect** retornará SQL_NEED_DATA e antes de retornar um código de retorno diferente, o driver cancelará o processo de navegação de conexão e retorna a conexão para um estado desconectado.  
  
 Se um aplicativo chamar **SQLDisconnect** enquanto houver uma transação incompleta associada com o identificador de conexão, o driver retornará SQLSTATE 25000 (estado de transação inválido), indicando que a transação está inalterada e a conexão está aberta. Uma transação incompleta é aquele que não foi confirmada ou revertida com **SQLEndTran**.  
  
 Se um aplicativo chamar **SQLDisconnect** antes que ele tiver liberado todas as instruções associadas com a conexão, o driver, depois com êxito se desconecta da fonte de dados, libera essas instruções e descritores de todos os que foram alocado explicitamente na conexão. No entanto, se uma ou mais das instruções associadas a conexão ainda estão sendo executadas de forma assíncrona, **SQLDisconnect** retornará SQL_ERROR com um valor SQLSTATE HY010 (erro de sequência de função). Além disso, **SQLDisconnect** liberará todos os respectivos instruções e todos os descritores explicitamente alocados na conexão, se a conexão está em um estado suspenso ou se **SQLDisconnect** foi cancelada com êxito pelo **SQLCancelHandle**.  
  
 Para obter informações sobre como um aplicativo usa **SQLDisconnect**, consulte [desconectar-se de uma fonte de dados ou Driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="disconnecting-from-a-pooled-connection"></a>Desconectando de uma Conexão em pool  
 Se o pool de conexão está habilitado para um ambiente compartilhado e um aplicativo chama **SQLDisconnect** em uma conexão nesse ambiente, a conexão é retornada ao pool de conexão e ainda está disponível para outros componentes usando o mesmo ambiente compartilhado.  
  
## <a name="code-example"></a>Exemplo de código  
 Ver [programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md), [função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), e [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Conectando a uma fonte de dados usando uma caixa de diálogo ou de cadeia de caracteres de conexão|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Executar uma operação de confirmação ou reversão|[Função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Liberando um identificador de conexão|[Função SQLFreeConnect](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
