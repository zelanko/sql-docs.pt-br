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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5ea73919fbe90719d881fb43108ab1934933708
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301146"
---
# <a name="sqldisconnect-function"></a>Função SQLDisconnect
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLDisconnect** fecha a conexão associada a uma alça de conexão específica.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConexãoHandle*  
 [Entrada] Identificador de conexão.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLDisconnect** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e uma *alça* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLDisconnect** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01002|Erro de desconexão|Ocorreu um erro durante a desconexão. No entanto, a desconexão foi bem sucedida. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) A conexão especificada no argumento *ConnectionHandle* não estava aberta.|  
|25000|Estado de transação inválido|Havia uma transação em processo na conexão especificada pelo argumento *ConnectionHandle*. A transação permanece ativa.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A função foi chamada, e antes de ser executada a [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamada no *ConnectionHandle*. Em seguida, a função foi chamada novamente no *ConnectionHandle*.<br /><br /> A função foi chamada e antes de terminar de executar **o SQLCancelHandle** foi chamado no *ConnectionHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para um *StatementHandle* associado ao *ConnectionHandle* e ainda estava sendo executada quando **o SQLDisconnect** foi chamado.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *ConnectionHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para um *StatementHandle* associado ao *ConnectionHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação, e a conexão ainda estivesse ativa. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *ConnectionHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Se um aplicativo chamar **SQLDisconnect** depois **que o SQLBrowseConnect** retorna SQL_NEED_DATA e antes de retornar um código de retorno diferente, o driver cancela o processo de navegação de conexão e retorna a conexão para um estado não conectado.  
  
 Se um aplicativo chamar **SQLDisconnect** enquanto houver uma transação incompleta associada à alça de conexão, o driver retorna SQLSTATE 25000 (estado de transação inválido), indicando que a transação está inalterada e a conexão está aberta. Uma transação incompleta é aquela que não foi cometida ou revertida com **o SQLEndTran**.  
  
 Se um aplicativo chamar **sqldisconnect** antes de ter liberado todas as instruções associadas à conexão, o driver, depois de desconectar com sucesso da fonte de dados, libera essas declarações e todos os descritores que foram explicitamente alocados na conexão. No entanto, se uma ou mais das instruções associadas à conexão ainda estiverem sendo executadas de forma assíncrona, **o SQLDisconnect** retorna SQL_ERROR com um valor SQLSTATE de HY010 (erro de seqüência de função). Além disso, **o SQLDisconnect** liberará todas as declarações associadas e todos os descritores que foram explicitamente alocados na conexão, se a conexão estiver em um estado suspenso ou se **o SQLDisconnect** foi cancelado com sucesso pelo **SQLCancelHandle**.  
  
 Para obter informações sobre como um aplicativo usa **o SQLDisconnect,** consulte [Desconectar-se de uma fonte de dados ou driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="disconnecting-from-a-pooled-connection"></a>Desconectando-se de uma conexão agrupada  
 Se o pool de conexões estiver habilitado para um ambiente compartilhado e um aplicativo chamar **sqldisconnect** em uma conexão nesse ambiente, a conexão será devolvida ao pool de conexões e ainda está disponível para outros componentes usando o mesmo ambiente compartilhado.  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [O Programa Amostra ODBC,](../../../odbc/reference/sample-odbc-program.md)Função [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)e [Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando uma alça|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Conectando-se a uma fonte de dados usando uma seqüência de conexão ou caixa de diálogo|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Executando uma operação de confirmação ou reversão|[Função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Liberando uma alça de conexão|[Função SQLFreeConnect](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
