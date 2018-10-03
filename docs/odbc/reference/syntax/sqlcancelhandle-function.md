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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a814b15255a485bf6fbc28ad31d4e789f8482447
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662114"
---
# <a name="sqlcancelhandle-function"></a>Função SQLCancelHandle
**Conformidade com**  
 Versão introduzida: ODBC 3.8  
  
 Conformidade com padrões: nenhum  
  
 É esperado que a maioria dos drivers ODBC 3.8 (e posterior) implementará essa função. Se um driver não, uma chamada para **SQLCancelHandle** com uma conexão lidar com o *manipular* parâmetro retornará SQL_ERROR com uma mensagem e SQLSTATE dos IM001 ' Driver não oferece suporte a essa função ' uma chamada para **SQLCancelHandle** com uma instrução manipular como o *manipular* parâmetro será mapeado para uma chamada para **SQLCancel** pelo Gerenciador de Driver e pode ser processado se o driver implementa **SQLCancel**. Um aplicativo pode usar **SQLGetFunctions** para determinar se um driver suporta **SQLCancelHandle**.  
  
 **Resumo**  
 **SQLCancelHandle** cancela o processamento em uma conexão ou instrução. O Gerenciador de Driver mapeia uma chamada para **SQLCancelHandle** a uma chamada para **SQLCancel** quando *HandleType* é SQL_HANDLE_STMT.  
  
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
 [Entrada] A alça na qual cancelar o processamento.  
  
 Se *manipular* não é um identificador válido do tipo especificado por *HandleType*, **SQLCancelHandle** retorne SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLCancelHandle** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de Manipulam SQL_HANDLE_STMT e uma instrução *manipular* ou um *HandleType* de SQL_HANDLE_DBC e um identificador de conexão *manipular*.  
  
 A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLCancelHandle** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) no argumento  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|Uma função de execução assíncrona, relacionados a instrução foi chamada para uma das alças de instrução associadas com o *manipular*, e *HandleType* foi definido como SQL_HANDLE_DBC. A função assíncrona ainda estava em execução quando **SQLCancelHandle** foi chamado.<br /><br /> (DM) a *HandleType* argumento era SQL_HANDLE_STMT; uma função de execução assíncrona foi chamada no identificador de conexão associados; e a função ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para uma das alças de instrução associadas com o *manipular* e *HandleType* foi definido como SQL_HANDLE_DBC e retornado SQL_PARAM_DATA_AVAILABLE. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> **SQLBrowseConnect** foi chamado para *ConnectionHandle*e retornada SQL_NEED_DATA. Essa função foi chamada antes do processo de navegação foi concluído.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY092|Identificador de atributo/opção inválido|*HandleType* foi definido como SQL_HANDLE_ENV ou SQL_HANDLE_DESC.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver de (DM) associado com o *manipular* não suporta a função.|  
  
 Se **SQLCancelHandle** for chamado com *HandleType* definido como SQL_HANDLE_STMT, ele pode retornar qualquer SQLSTATE que pode ser retornado pela função **SQLCancel**.  
  
## <a name="comments"></a>Comentários  
 Essa função é semelhante à **SQLCancel** , mas pode levar a alça de uma conexão ou uma instrução como um parâmetro em vez de apenas um identificador de instrução. O Gerenciador de Driver mapeia uma chamada para **SQLCancelHandle** a uma chamada para **SQLCancel** quando *HandleType* é SQL_HANDLE_STMT. Isso permite que aplicativos usem **SQLCancelHandle** cancelar operações de instrução, mesmo se o driver não implementa **SQLCancelHandle**.  
  
 Para obter mais informações sobre como cancelar uma operação de instrução, consulte [função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md).  
  
 Se não houver nenhuma operação em andamento na *manipular* a chamada para **SQLCancelHandle** não tem nenhum efeito.  
  
 **SQLCancelHandle** em uma conexão identificador pode cancelar os seguintes tipos de processamento:  
  
-   Uma função em execução de forma assíncrona na conexão.  
  
-   Uma função em execução no identificador de conexão em outro thread.  
  
 Quando **SQLCancelHandle** é chamado para cancelar uma função em execução assíncrona em uma conexão, os registros de diagnóstico postados por **SQLCancelHandle** são acrescentados aos retornados pela operação que está sendo cancelado; **SQLCancelHandle** não retorna registros de diagnóstico, no entanto, quando o cancelamento de uma função em execução em uma conexão em outro thread.  
  
 Usando o **SQLCancelHandle** Cancelar **SQLEndTran** pode colocar a conexão em um estado suspenso. Para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  Para obter informações sobre como usar **SQLCancelHandle** em um aplicativo que será implantado em um sistema de operacional Windows mais antigo que o Windows 7, consulte [matriz de compatibilidade](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>Cancelando Conexão relacionados ao processamento assíncrono  
 Se uma função retorna SQL_STILL_EXECUTING, um aplicativo pode chamar **SQLCancelHandle** para cancelar a operação. Se a solicitação de cancelamento for bem-sucedida, **SQLCancelHandle** retorna SQL_SUCCESS. Isso não significa que a função original foi cancelada; ele indica que a solicitação de cancelamento foi processada. O driver e a fonte de dados determinam quando ou se a operação foi cancelada. O aplicativo deve continuar a chamar a função original até que o código de retorno não seja SQL_STILL_EXECUTING. Se a função original tiver sido cancelada, o código de retorno é SQL_ERROR e SQLSTATE HY008 (operação cancelada). Se a função original concluído o processamento normal (não foi cancelado), o código de retorno é SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, ou SQL_ERROR e um SQLSTATE diferente HY008 (operação cancelada), se a falha da função original.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>Cancelando a funções em execução em outro Thread  
 Em um aplicativo multithread, o aplicativo pode cancelar uma operação que está em execução em outro thread. Para cancelar a operação, o aplicativo chama **SQLCancelHandle** com o identificador usado pela função, mas em um thread diferente. O driver e o sistema operacional determinam como a operação será cancelada. O **SQLCancelHandle** retornar o código que indica se o driver processa a solicitação, retornando SQL_SUCCESS ou SQL_ERROR (nenhuma informação de diagnóstico é retornada). Se o processamento na função original é cancelado, a função original retorna SQL_ERROR e SQLSTATE HY008 (operação cancelada).  
  
 Se uma função está sendo executado quando **SQLCancelHandle** é chamado em outro thread para cancelar a função, é possível que a função seja bem-sucedida e retorne SQL_SUCCESS antes que o cancelamento entre em vigor. Uma chamada para **SQLCancelHandle** não tem nenhum efeito se a operação é concluída antes de **SQLCancelHandle** foi capaz de cancelar a operação.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelando uma função em execução de forma assíncrona em um identificador de instrução, o cancelamento de uma função em uma instrução que precisa de dados ou cancelamento de uma função em execução em uma instrução em outro thread.|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
