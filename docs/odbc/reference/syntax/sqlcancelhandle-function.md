---
title: Função SQLCancelHandle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7abc9f9d515a77de67ecafc0e4193e055383f1b7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlcancelhandle-function"></a>Função SQLCancelHandle
**Conformidade**  
 Versão introduzidas: ODBC 3.8  
  
 Conformidade com padrões: nenhum  
  
 É esperado que a maioria dos drivers ODBC 3.8 (e posterior) implementar essa função. Se um driver não, uma chamada para **SQLCancelHandle** com uma conexão tratam o *tratar* parâmetro retornará SQL_ERROR com uma mensagem e SQLSTATE de IM001 ' Driver não dá suporte a essa função ' uma chamada para **SQLCancelHandle** com uma instrução tratar como o *tratar* parâmetro será mapeado para uma chamada para **SQLCancel** pelo Gerenciador de Driver e pode ser processada se o driver implementa **SQLCancel**. Um aplicativo pode usar **SQLGetFunctions** para determinar se um driver suporta **SQLCancelHandle**.  
  
 **Resumo**  
 **SQLCancelHandle** cancela o processamento em uma conexão ou instrução. O Gerenciador de Driver mapeia uma chamada para **SQLCancelHandle** para uma chamada para **SQLCancel** quando *HandleType* é SQL_HANDLE_STMT.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] O tipo do identificador no qual a cacel processamento. Os valores válidos são SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
 *Handle*  
 [Entrada] O identificador na qual cancelar o processamento.  
  
 Se *tratar* não é um identificador válido do tipo especificado pelo *HandleType*, **SQLCancelHandle** retorne SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLCancelHandle** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de Tratar SQL_HANDLE_STMT e uma instrução *tratar* ou um *HandleType* de SQL_HANDLE_DBC e um identificador de conexão *tratar*.  
  
 A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLCancelHandle** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) no argumento  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|Uma função de execução assíncrona, relacionadas a instrução foi chamada para uma das alças de instrução associadas a *tratar*, e *HandleType* foi definido como SQL_HANDLE_DBC. A função assíncrona ainda estava em execução quando **SQLCancelHandle** foi chamado.<br /><br /> (DM) a *HandleType* argumento foi SQL_HANDLE_STMT; uma função de execução assíncrona foi chamada no identificador de conexão associados; e a função ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para uma das alças de instrução associadas a *tratar* e *HandleType* foi definido como SQL_HANDLE_DBC e SQL_PARAM_DATA_AVAILABLE foi retornado. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> **SQLBrowseConnect** foi chamado para *identificador da conexão*e retorna SQL_NEED_DATA. Essa função foi chamada antes de concluir o processo de localização.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY092|Identificador de atributo/opção inválido|*HandleType* foi definido como SQL_HANDLE_ENV ou SQL_HANDLE_DESC.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *lidar com* não oferece suporte para a função.|  
  
 Se **SQLCancelHandle** é chamado com *HandleType* definido como SQL_HANDLE_STMT, ele pode retornar qualquer SQLSTATE que pode ser retornado pela função **SQLCancel**.  
  
## <a name="comments"></a>Comentários  
 Essa função é semelhante a **SQLCancel** , mas pode levar uma conexão ou instrução identificador como um parâmetro em vez de apenas um identificador de instrução. O Gerenciador de Driver mapeia uma chamada para **SQLCancelHandle** para uma chamada para **SQLCancel** quando *HandleType* é SQL_HANDLE_STMT. Isso permite que os aplicativos usem **SQLCancelHandle** cancelar operações de instrução, mesmo se o driver não implementa **SQLCancelHandle**.  
  
 Para obter mais informações sobre como cancelar uma operação de instrução, consulte [função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md).  
  
 Se não houver nenhuma operação em andamento em *tratar* a chamada para **SQLCancelHandle** não tem nenhum efeito.  
  
 **SQLCancelHandle** em uma conexão identificador pode cancelar os seguintes tipos de processamento:  
  
-   Uma função em execução de forma assíncrona na conexão.  
  
-   Uma função em execução no identificador da conexão em outro thread.  
  
 Quando **SQLCancelHandle** é chamado para cancelar uma função em execução assíncrona em uma conexão, os registros de diagnóstico postados por **SQLCancelHandle** são anexados aos retornados pela operação que está sendo cancelado; **SQLCancelHandle** não retorna registros de diagnóstico, no entanto, quando o cancelamento de uma função em execução em uma conexão em outro thread.  
  
 Usando **SQLCancelHandle** Cancelar **SQLEndTran** pode colocar a conexão em um estado suspenso. Para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  Para obter informações sobre como usar **SQLCancelHandle** em um aplicativo que será implantado em um sistema operacional do Windows anterior ao Windows 7, consulte [matriz de compatibilidade](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>Cancelando o processamento assíncrono relacionadas à Conexão  
 Se uma função retorna SQL_STILL_EXECUTING, um aplicativo pode chamar **SQLCancelHandle** para cancelar a operação. Se a solicitação de cancelamento for bem-sucedida, **SQLCancelHandle** retorna SQL_SUCCESS. Isso não significa que a função original foi cancelada; indica que a solicitação de cancelamento foi processada. O driver e a fonte de dados determinam quando ou se a operação foi cancelada. O aplicativo deve continuar a chamar a função original até que o código de retorno não é SQL_STILL_EXECUTING. Se a função original foi cancelada, o código de retorno é SQL_ERROR e SQLSTATE HY008 (operação cancelada). Se a função original concluiu o processamento normal (não foi cancelado), o código de retorno é SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, ou SQL_ERROR e um SQLSTATE diferente HY008 (operação cancelada), se a função original falhou.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>Cancelando funções em execução em outro Thread  
 Em um aplicativo multithread, o aplicativo pode cancelar uma operação que está sendo executado em outro thread. Para cancelar a operação, o aplicativo chama **SQLCancelHandle** com o identificador usado pela função, mas em um thread diferente. O driver e sistema operacional determinam como a operação foi cancelada. O **SQLCancelHandle** retornam o código que indica se o driver processa a solicitação, retornando SQL_SUCCESS ou SQL_ERROR (nenhuma informação de diagnóstica é retornada). Se o processamento na função original é cancelado, a função original retornará SQL_ERROR e SQLSTATE HY008 (operação cancelada).  
  
 Se uma função está sendo executado quando **SQLCancelHandle** é chamado em outro thread para cancelar a função, é possível que a função ter êxito e retornar SQL_SUCCESS para o cancelamento entre em vigor. Uma chamada para **SQLCancelHandle** não tem efeito se a operação foi concluída antes de **SQLCancelHandle** conseguiu cancelar a operação.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelando uma função em execução assíncrona em um identificador de instrução, cancelamento de uma função em uma instrução que precisa de dados, ou cancelar uma função em execução em uma instrução em outro thread.|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
