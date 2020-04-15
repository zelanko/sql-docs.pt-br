---
title: Função SQLCancelHandle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 059ed283032feb96ca5e6b12520682ccb034752a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299661"
---
# <a name="sqlcancelhandle-function"></a>Função SQLCancelHandle
**Conformidade**  
 Versão introduzida: ODBC 3.8  
  
 Conformidade com as normas: nenhuma  
  
 Espera-se que a maioria dos drivers ODBC 3.8 (e posteriores) implemente essa função. Se um driver não fizer isso, uma chamada para **SQLCancelHandle** com uma alça de conexão no parâmetro *Handle* retornará SQL_ERROR com um SQLSTATE de IM001 e a mensagem 'Driver não suporta essa função'' Uma chamada para **SQLCancelHandle** com uma alça de declaração, pois o parâmetro *Handle* será mapeado para uma chamada para **SQLCancel** pelo Driver Manager e pode ser processado se o driver implementar **SQLCancel**. Um aplicativo pode usar **SQLGetFunctions** para determinar se um driver suporta **SQLCancelHandle**.  
  
 **Resumo**  
 **O SQLCancelHandle** cancela o processamento em uma conexão ou declaração. O Gerenciador de driver mapeia uma chamada para **SQLCancelHandle** para uma chamada para **SQLCancel** quando *handleType* é SQL_HANDLE_STMT.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Handletype*  
 [Entrada] O tipo de alça sobre a qual o processamento de cacel. Os valores válidos são SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
 *Handle*  
 [Entrada] A alça sobre a qual cancelar o processamento.  
  
 Se *o Handle* não for uma alça válida do tipo especificado pelo *HandleType,* **o SQLCancelHandle** retorna SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLCancelHandle** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *handle handle de* declaração ou um *HandleType* de SQL_HANDLE_DBC e uma *alça*de conexão .  
  
 A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLCancelHandle** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) no argumento * \*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|Uma função assíncronamente executada, relacionada à declaração, foi chamada para uma das alças de declaração associadas ao *Handle*, e *handleType* foi definido como SQL_HANDLE_DBC. A função assíncrona ainda estava sendo executada quando **o SQLCancelHandle** foi chamado.<br /><br /> (DM) O argumento *HandleType* foi SQL_HANDLE_STMT; uma função de execução assíncrona foi chamada no cabo de conexão associado; e a função ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foi chamado para que uma das alças de declaração associadas ao *Handle* and *HandleType* fosse definida como SQL_HANDLE_DBC e retornasse SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> **O SQLBrowseConnect** foi chamado para *o ConnectionHandle*e retornou SQL_NEED_DATA. Esta função foi chamada antes do processo de navegação ser concluído.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY092|Identificador de atributo/opção inválido|*HandleType* foi definido para SQL_HANDLE_ENV ou SQL_HANDLE_DESC.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado à *alça* não suporta a função.|  
  
 Se **o SQLCancelHandle** for chamado com *handleType* definido para SQL_HANDLE_STMT, ele poderá retornar qualquer SQLSTATE que possa ser retornado pela função **SQLCancel**.  
  
## <a name="comments"></a>Comentários  
 Esta função é semelhante ao **SQLCancel,** mas pode ter uma conexão ou uma alça de declaração como parâmetro, em vez de apenas uma alça de declaração. O Gerenciador de driver mapeia uma chamada para **SQLCancelHandle** para uma chamada para **SQLCancel** quando *handleType* é SQL_HANDLE_STMT. Isso permite que os aplicativos usem **o SQLCancelHandle** para cancelar operações de declaração mesmo que o driver não implemente **o SQLCancelHandle**.  
  
 Para obter mais informações sobre o cancelamento de uma operação de declaração, consulte [SQLCancel Function](../../../odbc/reference/syntax/sqlcancel-function.md).  
  
 Se não houver operações em andamento no *Handle,* a chamada para **SQLCancelHandle** não tem efeito.  
  
 **SQLCancelHandle** em uma alça de conexão pode cancelar os seguintes tipos de processamento:  
  
-   Uma função em execução assíncrona na conexão.  
  
-   Uma função em execução na alça de conexão em outro segmento.  
  
 Quando **o SQLCancelHandle** é chamado a cancelar uma função em execução assíncrona em uma conexão, os registros de diagnóstico publicados pelo **SQLCancelHandle** são anexados àqueles devolvidos pela operação que está sendo cancelada; **SQLCancelHandle** não retorna registros de diagnóstico, no entanto, ao cancelar uma função em execução em uma conexão em outro segmento.  
  
 O uso **do SQLCancelHandle** para cancelar o **SQLEndTran** pode colocar a conexão em estado suspenso. Para obter mais informações sobre o estado suspenso, consulte [SQLEndTran Function](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  Para obter informações sobre como usar **o SQLCancelHandle** em um aplicativo que será implantado em um sistema operacional Windows mais antigo que o Windows 7, consulte [Matrix de compatibilidade](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>Cancelando o processamento assíncrono relacionado à conexão  
 Se uma função retornar SQL_STILL_EXECUTING, um aplicativo pode ligar para **o SQLCancelHandle** para cancelar a operação. Se a solicitação de cancelamento for bem sucedida, **o SQLCancelHandle** retorna SQL_SUCCESS. Isso não significa que a função original foi cancelada; indica que o pedido de cancelamento foi processado. O driver e a fonte de dados determinam quando ou se a operação é cancelada. O aplicativo deve continuar a chamar a função original até que o código de retorno não seja SQL_STILL_EXECUTING. Se a função original foi cancelada, o código de devolução será SQL_ERROR e SQLSTATE HY008 (Operação cancelada). Se a função original completou seu processamento normal (não foi cancelada), o código de retorno será SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, ou SQL_ERROR e um SQLSTATE diferente de HY008 (Operação cancelada), se a função original falhar.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>Cancelando funções executando em outro segmento  
 Em um aplicativo multithread, o aplicativo pode cancelar uma operação que está sendo executado em outro segmento. Para cancelar a operação, o aplicativo chama **SQLCancelHandle** com a alça usada pela função, mas em um segmento diferente. O driver e o sistema operacional determinam como a operação é cancelada. O código de retorno **SQLCancelHandle** indica se o driver processou a solicitação, retornando SQL_SUCCESS ou SQL_ERROR (nenhuma informação de diagnóstico é retornada). Se o processamento na função original for cancelado, a função original reatornou SQL_ERROR e SQLSTATE HY008 (Operação cancelada).  
  
 Se uma função estiver sendo executada quando **o SQLCancelHandle** for chamado em outro segmento para cancelar a função, é possível que a função tenha sucesso e retorne SQL_SUCCESS antes que o cancelamento possa entrar em vigor. Uma chamada para **SQLCancelHandle** não tem efeito se a operação concluída antes **do SQLCancelHandle** conseguir cancelar a operação.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelando uma função em execução assíncrona em uma alça de declaração, cancelando uma função em uma declaração que precisa de dados ou cancelando uma função em execução em uma declaração em outro segmento.|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Execução Assíncrona (Método de Votação)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
