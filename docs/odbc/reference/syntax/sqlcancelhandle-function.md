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
ms.openlocfilehash: b3f9dcb6ccdef290b937b1317271758dddc0e848
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279596"
---
# <a name="sqlcancelhandle-function"></a>Função SQLCancelHandle
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,8: nenhuma  
  
 Espera-se que a maioria dos drivers ODBC 3,8 (e posteriores) Implemente essa função. Se um driver não for, uma chamada para **SQLCancelHandle** com um identificador de conexão no *parâmetro Handle* retornará SQL_ERROR com um SQLSTATE de IM001 e o driver Message ' não oferece suporte a essa função ' ' uma chamada **para SQLCancelHandle** com um identificador de instrução, pois o parâmetro *Handle* será mapeado para uma chamada para **SQLCancel** pelo Gerenciador de driver e poderá ser processado se o driver implementar **SQLCancel**. Um aplicativo pode usar **SQLGetFunctions** para determinar se um driver dá suporte a **SQLCancelHandle**.  
  
 **Resumo**  
 **SQLCancelHandle** cancela o processamento em uma conexão ou instrução. O Gerenciador de driver mapeia uma chamada para **SQLCancelHandle** para uma chamada para **SQLCancel** quando *HandleType* é SQL_HANDLE_STMT.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 Entrada O tipo do identificador no qual cacel o processamento. Os valores válidos são SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
 *Handle*  
 Entrada O identificador no qual cancelar o processamento.  
  
 Se o *identificador* não for um identificador válido do tipo especificado por *HandleType*, **SQLCancelHandle** retornará SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLCancelHandle** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um identificador de identificador de *instrução ou um* *identificador* de SQL_HANDLE_DBC e um identificador de identificador de *conexão.*  
  
 A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLCancelHandle** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) no argumento * \* MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|Uma função de execução assíncrona, relacionada a instruções, foi chamada para um dos identificadores de instrução associados ao *identificador*e o *HandleType* foi definido como SQL_HANDLE_DBC. A função assíncrona ainda estava em execução quando **SQLCancelHandle** foi chamado.<br /><br /> (DM) o argumento *HandleType* foi SQL_HANDLE_STMT; uma função de execução assíncrona foi chamada no identificador de conexão associado; e a função ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para um dos identificadores de instrução associados ao *identificador* e ao *HandleType* definido como SQL_HANDLE_DBC e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> **SQLBrowseConnect** foi chamado para *ConnectionHandle*e retornou SQL_NEED_DATA. Esta função foi chamada antes da conclusão do processo de navegação.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY092|Identificador de atributo/opção inválido|*HandleType* foi definido como SQL_HANDLE_ENV ou SQL_HANDLE_DESC.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *identificador* não oferece suporte à função.|  
  
 Se **SQLCancelHandle** for chamado com *HandleType* definido como SQL_HANDLE_STMT, ele poderá retornar qualquer SQLSTATE que possa ser retornado pela função **SQLCancel**.  
  
## <a name="comments"></a>Comentários  
 Essa função é semelhante a **SQLCancel** , mas pode levar um identificador de conexão ou de instrução como um parâmetro, em vez de apenas um identificador de instrução. O Gerenciador de driver mapeia uma chamada para **SQLCancelHandle** para uma chamada para **SQLCancel** quando *HandleType* é SQL_HANDLE_STMT. Isso permite que os aplicativos usem o **SQLCancelHandle** para cancelar operações de instrução mesmo que o driver não implemente **SQLCancelHandle**.  
  
 Para obter mais informações sobre como cancelar uma operação de instrução, consulte [função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md).  
  
 Se não houver nenhuma operação em andamento na *manipulação* da chamada para **SQLCancelHandle** não terá nenhum efeito.  
  
 **SQLCancelHandle** em um identificador de conexão pode cancelar os seguintes tipos de processamento:  
  
-   Uma função que executa de forma assíncrona na conexão.  
  
-   Uma função em execução no identificador de conexão em outro thread.  
  
 Quando **SQLCancelHandle** é chamado para cancelar uma função que executa de forma assíncrona em uma conexão, os registros de diagnóstico postados por **SQLCancelHandle** são anexados aos retornados pela operação que está sendo cancelada; No entanto, o **SQLCancelHandle** não retorna registros de diagnóstico ao cancelar uma função em execução em uma conexão em outro thread.  
  
 Usar **SQLCancelHandle** para cancelar **SQLEndTran** pode colocar a conexão no estado suspenso. Para obter mais informações sobre o estado suspenso, consulte a [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  Para obter informações sobre como usar o **SQLCancelHandle** em um aplicativo que será implantado em um sistema operacional Windows mais antigo que o Windows 7, consulte [matriz de compatibilidade](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>Cancelando o processamento assíncrono relacionado à conexão  
 Se uma função retornar SQL_STILL_EXECUTING, um aplicativo poderá chamar **SQLCancelHandle** para cancelar a operação. Se a solicitação de cancelamento for bem-sucedida, **SQLCancelHandle** retornará SQL_SUCCESS. Isso não significa que a função original foi cancelada; Isso indica que a solicitação de cancelamento foi processada. O driver e a fonte de dados determinam quando ou se a operação foi cancelada. O aplicativo deve continuar a chamar a função original até que o código de retorno não seja SQL_STILL_EXECUTING. Se a função original foi cancelada, o código de retorno será SQL_ERROR e SQLSTATE HY008 (operação cancelada). Se a função original tiver concluído seu processamento normal (não foi cancelada), o código de retorno será SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, ou SQL_ERROR e um SQLSTATE diferente de HY008 (operação cancelada), se a função original tiver falhado.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>Cancelando funções em execução em outro thread  
 Em um aplicativo multithread, o aplicativo pode cancelar uma operação em execução em outro thread. Para cancelar a operação, o aplicativo chama **SQLCancelHandle** com o identificador usado pela função, mas em um thread diferente. O driver e o sistema operacional determinam como a operação é cancelada. O código de retorno **SQLCancelHandle** indica se o driver processou a solicitação, retornando SQL_SUCCESS ou SQL_ERROR (nenhuma informação de diagnóstico é retornada). Se o processamento na função original for cancelado, a função original retornará SQL_ERROR e SQLSTATE HY008 (operação cancelada).  
  
 Se uma função estiver sendo executada quando **SQLCancelHandle** for chamado em outro thread para cancelar a função, será possível que a função seja bem sucedido e retorne SQL_SUCCESS antes que o cancelamento entre em vigor. Uma chamada para **SQLCancelHandle** não terá efeito se a operação for concluída antes que **SQLCancelHandle** pudesse cancelar a operação.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelando uma função que executa de forma assíncrona em um identificador de instrução, cancelando uma função em uma instrução que precisa de dados ou cancelando uma função em execução em uma instrução em outro thread.|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
