---
title: "Função SQLDisconnect | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: af65dee0cfa0efcb4b4daffa55e02dfbebff8473
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqldisconnect-function"></a>Função SQLDisconnect
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLDisconnect** fecha a conexão associada a um identificador de conexão específica.  
  
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
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLDisconnect** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_DBC e um *tratar* de *identificador da conexão*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDisconnect** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01002|Erro de desconexão|Ocorreu um erro durante a desconexão. No entanto, a desconexão foi bem-sucedida. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) a conexão especificada no argumento *identificador da conexão* não foi aberto.|  
|25000|Estado de transação inválido|Houve uma transação em processo em que a conexão especificada pelo argumento *identificador da conexão*. A transação permanece ativa.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *identificador da conexão*. A função foi chamada, e antes de executar terminou [SQLCancelHandle função](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamado no *identificador da conexão*. Em seguida, a função foi chamada novamente no *identificador da conexão*.<br /><br /> A função foi chamada e antes ele terminar a execução **SQLCancelHandle** foi chamado no *identificador da conexão* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para um *StatementHandle* associados a *identificador da conexão* e ainda estava em execução quando **SQLDisconnect** foi chamado.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *identificador da conexão* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para um *StatementHandle*  associados a *identificador da conexão* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação, e a conexão ainda está ativa. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *identificador da conexão* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Se um aplicativo chamar **SQLDisconnect** depois **SQLBrowseConnect** retorna SQL_NEED_DATA e antes de retornar um código de retorno diferente, o driver cancelará o processo de pesquisa de conexão e retorna a conexão para um estado desconectado.  
  
 Se um aplicativo chamar **SQLDisconnect** enquanto houver uma transação incompleta associada ao identificador de conexão, o driver retornará SQLSTATE 25000 (estado de transação inválido), indicando que a transação está inalterada e a conexão está aberta. Uma transação incompleta é aquele que não foi confirmada ou revertida com **SQLEndTran**.  
  
 Se um aplicativo chamar **SQLDisconnect** antes de liberar todas as instruções associadas a conexão, o driver depois com êxito se desconecta da fonte de dados, libera essas instruções e todos os descritores que foram alocado explicitamente a conexão. No entanto, se um ou mais instruções associadas a conexão ainda estão em execução em modo assíncrono, **SQLDisconnect** retornará SQL_ERROR com um valor SQLSTATE HY010 (erro de sequência de função). Além disso, **SQLDisconnect** irá liberar todos os respectivos instruções e todos os descritores que foram explicitamente alocados na conexão, se a conexão está em um estado suspenso ou se **SQLDisconnect** foi cancelado com êxito pelo **SQLCancelHandle**.  
  
 Para obter informações sobre como um aplicativo usa **SQLDisconnect**, consulte [desconectar-se de uma fonte de dados ou Driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="disconnecting-from-a-pooled-connection"></a>Desconectando de uma Conexão em pool  
 Se o pool de conexão está habilitado para um ambiente compartilhado, e um aplicativo chama **SQLDisconnect** em uma conexão nesse ambiente, a conexão é retornado para o pool de conexão e ainda está disponível para outros componentes usando o mesmo ambiente compartilhado.  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [ODBC programa de exemplo](../../../odbc/reference/sample-odbc-program.md), [função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), e [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Conectando a uma fonte de dados usando uma caixa de diálogo ou cadeia de caracteres de conexão|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Executar uma operação de confirmação ou reversão|[Função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Liberando um identificador de conexão|[Função SQLFreeConnect](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)

