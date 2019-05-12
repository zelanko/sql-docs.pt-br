---
title: Função SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0d92abe17128bff382d4b291fa9d20fe5c4fa77
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536635"
---
# <a name="sqlparamdata-function"></a>Função SQLParamData
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLParamData** é usada junto com **SQLPutData** para fornecer dados de parâmetro durante o tempo de execução de instrução e com **SQLGetData** para recuperar dados de parâmetro de saída transmitidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *ValuePtrPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o endereço do *ParameterValuePtr* buffer especificado em **SQLBindParameter** (para dados de parâmetro) ou o endereço do *TargetValuePtr* buffer especificado no **SQLBindCol** (para dados de coluna), conforme contido no campo de registro do descritor SQL_DESC_DATA_PTR.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLParamData** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLParamData** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|O valor de dados identificado pela *ValueType* argumento **SQLBindParameter** para o parâmetro associado não pôde ser convertido para o tipo de dados identificado pelo *ParameterType*argumento na **SQLBindParameter**.<br /><br /> O valor dos dados retornados para um parâmetro associado como SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT não pôde ser convertido para o tipo de dados identificado pelo *ValueType* argumento **SQLBindParameter**.<br /><br /> (Se os valores de dados para uma ou mais linhas não pôde ser convertidos, mas uma ou mais linhas foram retornadas com êxito, essa função retorna SQL_SUCCESS_WITH_INFO).|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|22026|Incompatibilidade de comprimento de dados String|O tipo de informação no SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "Y", e menos dados foi enviados para um parâmetro longo (o tipo de dados era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específicos da fonte de dados longos) que foi especificado com o *StrLen_or_IndPtr* argumento **SQLBindParameter**.<br /><br /> O tipo de informação no SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "Y", e menos dados foi enviados para uma coluna long (tipo de dados era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específicos da fonte de dados longos) que foi especificada no buffer de comprimento correspondente a uma coluna em uma linha de dados que foram adicionados ou atualizados com **SQLBulkOperations** ou foram atualizados com **SQLSetPos**.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão desconhecida de declaração|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*; a função foi chamada, em seguida, novamente em o *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) a chamada de função anterior não era uma chamada para **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, ou **SQLSetPos** onde o retornar o código foi SQL_NEED_DATA ou chamada de função anterior foi uma chamada para **SQLPutData**.<br /><br /> A chamada de função anterior foi uma chamada para **SQLParamData**.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLParamData** função foi chamada.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o *StatementHandle* e SQL_NEED_DATA retornado. **SQLCancel** foi chamado antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|(DM) o driver que corresponde do *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
 Se **SQLParamData** é chamado durante o envio de dados para um parâmetro em uma instrução SQL, ele pode retornar qualquer SQLSTATE que pode ser retornado pela função chamada para executar a instrução (**SQLExecute** ou **SQLExecDirect**). Se for chamado durante o envio de dados de uma coluna que está sendo atualizada ou adicionada com **SQLBulkOperations** ou que está sendo atualizada com **SQLSetPos**, ele pode retornar qualquer SQLSTATE que pode ser retornado por  **SQLBulkOperations** ou **SQLSetPos**.  
  
## <a name="comments"></a>Comentários  
 **SQLParamData** pode ser chamado para fornecer dados de dados em execução para dois usos: dados de parâmetro que serão usados em uma chamada para **SQLExecute** ou **SQLExecDirect**, ou dados da coluna que serão usado quando uma linha é atualizada ou adicionada por uma chamada para **SQLBulkOperations** ou atualizados por uma chamada para **SQLSetPos**. Em tempo de execução **SQLParamData** retorna para o aplicativo requer que um indicador de quais dados o driver.  
  
 Quando um aplicativo chama **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos**, o driver retorna SQL_NEED_ DADOS se precisar de dados de dados em execução. Um aplicativo, em seguida, chama **SQLParamData** para determinar quais dados a serem enviados. Se o driver requer dados de parâmetro, o driver retorna na  *\*ValuePtrPtr* o valor que o aplicativo é colocado no buffer de conjunto de linhas do buffer de saída. O aplicativo pode usar esse valor para determinar quais dados de parâmetro, o driver está solicitando. Se o driver requer dados da coluna, o driver retorna na  *\*ValuePtrPtr* armazenar em buffer o endereço ao qual a coluna foi originalmente vinculada, da seguinte maneira:  
  
 *Ligado a endereço* + *associação deslocamento* + ((*número de linha* - 1) x *tamanho do elemento*)  
  
 onde as variáveis são definidas como indicado na tabela a seguir.  
  
|Variável|Descrição|  
|--------------|-----------------|  
|*Ligado a endereço*|O endereço especificado com o *TargetValuePtr* argumento **SQLBindCol**.|  
|*Deslocamento de associação*|O valor armazenado no endereço especificado com o atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR.|  
|*Número de linha*|O número da linha no conjunto de linhas de base 1. Para buscas de única linha, que são o padrão, isso é 1.|  
|*Tamanho do elemento*|O valor do atributo de instrução SQL_ATTR_ROW_BIND_TYPE para buffers de dados e comprimento/indicador.|  
  
 Ele também retorna SQL_NEED_DATA, que é um indicador para o aplicativo que ele deverá chamar **SQLPutData** para enviar os dados.  
  
 O aplicativo chama **SQLPutData** como quantas vezes forem necessárias para enviar os dados de dados em execução para a coluna ou parâmetro. Depois que todos os dados foram enviadas para a coluna ou parâmetro, o aplicativo chama **SQLParamData** novamente. Se **SQLParamData** novamente retorna SQL_NEED_DATA, dados devem ser enviados para o outro parâmetro ou coluna. Portanto, o aplicativo novamente chama **SQLPutData**. Se todos os dados de dados em execução tiver sido enviado para todos os parâmetros ou colunas, em seguida **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o valor na  *\*ValuePtrPtr* é indefinida, e pode ser executada a instrução SQL ou o **SQLBulkOperations** ou **SQLSetPos** chamada pode ser processada.  
  
 Se **SQLParamData** fontes de dados de parâmetro para um pesquisada instrução update ou delete que não afeta nenhuma linha na fonte de dados, a chamada para **SQLParamData** retorne SQL_NO_DATA.  
  
 Para obter mais informações sobre os dados de parâmetro como dados em execução são passadas em tempo de execução de instrução, consulte "Passando valores de parâmetro" na [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [enviando dados Long](../../../odbc/reference/develop-app/sending-long-data.md). Para obter mais informações sobre os dados da coluna como dados em execução são atualizadas ou adicionadas, consulte a seção "Usando SQLSetPos" em [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Executando em massa atualizações usando indicadores" no [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), e [dados Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
 **SQLParamData** pode ser chamado para recuperar parâmetros de saída em fluxo. Quando **SQLMoreResults**, **SQLExecute**, **SQLGetData**, ou **SQLExecDirect** retorna SQL_PARAM_DATA_AVAILABLE, chamada **SQLParamData** para determinar qual parâmetro tem um valor disponível. Para obter mais informações sobre parâmetros de saída transmitidos e SQL_PARAM_DATA_AVAILABLE, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Ver [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre um parâmetro em uma instrução|[Função SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Enviar dados de parâmetro em tempo de execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
