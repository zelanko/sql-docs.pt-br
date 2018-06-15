---
title: Função SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLParamData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLParamData
helpviewer_keywords:
- SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2debf8a85ad31533995613c5e06c17a6e4040d5a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32921901"
---
# <a name="sqlparamdata-function"></a>Função SQLParamData
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLParamData** é usado junto com **SQLPutData** para fornecer dados de parâmetro em tempo de execução de instrução e com **SQLGetData** para recuperar dados de parâmetro de saída transmitidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *ValuePtrPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o endereço do *ParameterValuePtr* buffer especificado em **SQLBindParameter** (para os dados de parâmetro) ou o endereço do *TargetValuePtr* buffer especificado em **SQLBindCol** (para a coluna de dados), como contida no campo de registro do descritor SQL_DESC_DATA_PTR.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLParamData** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLParamData** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|O valor de dados identificado pelo *ValueType* argumento **SQLBindParameter** para o parâmetro associado não pôde ser convertido para o tipo de dados identificado pelo *ParameterType*argumento **SQLBindParameter**.<br /><br /> O valor dos dados retornados para um parâmetro associado como SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT não pôde ser convertido para o tipo de dados identificado pelo *ValueType* argumento **SQLBindParameter**.<br /><br /> (Se não foi possível converter os valores de dados para uma ou mais linhas, mas uma ou mais linhas foram retornadas com êxito, essa função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|22026|Incompatibilidade de comprimento de dados String|O tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo** foi "Y", e menos dados foi enviados para um parâmetro de tempo (o tipo de dados foi SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados de específico de fonte de dados longos) que foi especificada com o *StrLen_or_IndPtr* argumento **SQLBindParameter**.<br /><br /> O tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo** foi "Y", e menos dados foi enviados para uma coluna longa (o tipo de dados foi SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados de específico de fonte de dados longos) que foi especificada no buffer de comprimento correspondente a uma coluna em uma linha de dados que foram adicionados ou atualizados com **SQLBulkOperations** ou atualizada com **SQLSetPos**.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão de instrução desconhecido|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*; a função foi chamada novamente em o *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em uma aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) da chamada de função anterior não era uma chamada para **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, ou **SQLSetPos** onde o retornar código foi SQL_NEED_DATA ou chamada de função anterior foi uma chamada para **SQLPutData**.<br /><br /> A chamada de função anterior foi uma chamada para **SQLParamData**.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLParamData** função foi chamada.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o *StatementHandle* e SQL_NEED_DATA retornado. **SQLCancel** foi chamado antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|(DM) o driver que corresponde do *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
 Se **SQLParamData** é chamado durante o envio de dados para um parâmetro em uma instrução SQL, ele pode retornar qualquer SQLSTATE que pode ser retornado pela função chamada para executar a instrução (**SQLExecute** ou **SQLExecDirect**). Se ele é chamado durante o envio de dados de uma coluna que está sendo atualizada ou adicionadas **SQLBulkOperations** ou que está sendo atualizado com **SQLSetPos**, pode retornar qualquer SQLSTATE que pode ser retornado por  **SQLBulkOperations** ou **SQLSetPos**.  
  
## <a name="comments"></a>Comentários  
 **SQLParamData** pode ser chamado para fornecer dados de dados em execução para dois usos: dados de parâmetro que serão usados em uma chamada para **SQLExecute** ou **SQLExecDirect**, ou dados da coluna que serão usada quando uma linha é atualizada ou adicionada por uma chamada para **SQLBulkOperations** ou atualizada por uma chamada para **SQLSetPos**. Em tempo de execução, **SQLParamData** retorna para o aplicativo requer que um indicador de quais dados o driver.  
  
 Quando um aplicativo chama **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos**, o driver retorna SQL_NEED_ DADOS se precisar de dados de dados em execução. Um aplicativo, em seguida, chama **SQLParamData** para determinar quais dados a serem enviados. Se o driver requer dados de parâmetro, o driver retorna no  *\*ValuePtrPtr* o valor que o aplicativo é colocado no buffer de linhas do buffer de saída. O aplicativo pode usar esse valor para determinar quais dados de parâmetro, o driver está solicitando. Se o driver requer dados de coluna, o driver retorna no  *\*ValuePtrPtr* buffer o endereço que a coluna foi originalmente associada, da seguinte maneira:  
  
 *Ligado a endereço* + *associação deslocamento* + ((*linha número* – 1) x *tamanho do elemento*)  
  
 onde as variáveis são definidas conforme indicado na tabela a seguir.  
  
|Variável|Description|  
|--------------|-----------------|  
|*Ligado a endereço*|O endereço especificado com o *TargetValuePtr* argumento **SQLBindCol**.|  
|*Deslocamento de associação*|O valor armazenado no endereço especificado com o atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR.|  
|*Número de linha*|O número da linha no conjunto de linhas de base 1. Para buscas de única linha, que são o padrão, isso é 1.|  
|*Tamanho do elemento*|O valor do atributo de instrução SQL_ATTR_ROW_BIND_TYPE para buffers de dados e comprimento/indicador.|  
  
 Ele também retorna SQL_NEED_DATA, que é um indicador para o aplicativo deve chamar **SQLPutData** para enviar os dados.  
  
 O aplicativo chama **SQLPutData** quantas vezes forem necessárias para enviar os dados de dados em execução para a coluna ou parâmetro. Após ter sido enviada a todos os dados para a coluna ou parâmetro, o aplicativo chama **SQLParamData** novamente. Se **SQLParamData** novamente retorna SQL_NEED_DATA dados devem ser enviados para outro parâmetro ou coluna. Portanto, o aplicativo novamente chama **SQLPutData**. Se todos os dados de dados em execução foi enviada para todos os parâmetros ou colunas, em seguida, **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o valor em  *\*ValuePtrPtr* será indefinido, e a instrução SQL pode ser executada ou o **SQLBulkOperations** ou **SQLSetPos** chamada pode ser processada.  
  
 Se **SQLParamData** fontes de dados de parâmetro para um pesquisada instrução update ou delete que não afeta qualquer linha na fonte de dados, a chamada para **SQLParamData** retorna SQL_NO_DATA.  
  
 Para obter mais informações sobre os dados de parâmetro como dados em execução são passadas em tempo de execução de instrução, consulte "Valores de parâmetro passando" [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [enviar dados longos](../../../odbc/reference/develop-app/sending-long-data.md). Para obter mais informações sobre os dados da coluna de dados em execução como são atualizadas ou adicionadas, consulte a seção "Usando SQLSetPos" [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Executar em massa atualizações usando indicadores" [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), e [dados longos e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
 **SQLParamData** pode ser chamado para recuperar os parâmetros de saída em fluxo. Quando **SQLMoreResults**, **SQLExecute**, **SQLGetData**, ou **SQLExecDirect** retorna SQL_PARAM_DATA_AVAILABLE, chame **SQLParamData** para determinar qual parâmetro tem um valor disponível. Para obter mais informações sobre SQL_PARAM_DATA_AVAILABLE e parâmetros de saída em fluxo, consulte [recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre um parâmetro em uma instrução|[Função SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução preparada do SQL|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Envio de dados de parâmetro em tempo de execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
