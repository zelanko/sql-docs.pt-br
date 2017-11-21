---
title: RECEBER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RECEIVE_TSQL
- RECEIVE
dev_langs:
- TSQL
helpviewer_keywords:
- queues [Service Broker], message retrieval
- messages [Service Broker], retrieving
- RECEIVE statement
- receiving messages
- retrieving messages
ms.assetid: 878c6c14-37ab-4b87-9854-7f8f42bac7dd
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4cf66234550d32eafae1029d80c0330499d75553
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="receive-transact-sql"></a>RECEIVE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Recupera uma ou mais mensagens de uma fila. Dependendo da configuração de retenção da fila, essa instrução remove as mensagens da fila ou atualiza o status da mensagem na fila.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
[ WAITFOR ( ]  
    RECEIVE [ TOP ( n ) ]   
        <column_specifier> [ ,...n ]  
        FROM <queue>  
        [ INTO table_variable ]  
        [ WHERE {  conversation_handle = conversation_handle  
                 | conversation_group_id = conversation_group_id } ]  
[ ) ] [ , TIMEOUT timeout ]  
[ ; ]  
  
<column_specifier> ::=  
{    *   
  |  { column_name | [ ] expression } [ [ AS ] column_alias ]  
  |  column_alias = expression   
}     [ ,...n ]   
  
<queue> ::=  
{  
    [ database_name . [ schema_name ] . | schema_name . ]  
        queue_name  
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 WAITFOR  
 Especifica que a instrução RECEIVE aguardará a chegada de uma mensagem na fila, se não houver nenhuma mensagem no momento.  
  
 PARTE SUPERIOR (  *n*  )  
 Especifica o número máximo de mensagens a serem retornadas. Se essa cláusula não estiver especificada, todas as mensagens que atenderem aos critérios da instrução serão retornadas.  
  
 \*  
 Especifica que o conjunto de resultados contém todas as colunas na fila.  
  
 *nome da coluna*  
 O nome de uma coluna a ser incluído no conjunto de resultados.  
  
 *expressão*  
 Um nome de coluna, constante, função ou qualquer combinação de nomes de coluna, constantes e funções conectadas por um operador.  
  
 *column_alias*  
 Um nome alternativo para substituir o nome da coluna no conjunto de resultados.  
  
 FROM  
 Especifica a fila que contém as mensagens a serem recuperadas.  
  
 *database_name*  
 O nome do banco de dados que contém a fila da qual receber mensagens. Quando nenhum *nome do banco de dados* for fornecido, o padrão é o banco de dados atual.  
  
 *schema_name*  
 O nome do esquema que possui a fila da qual receber mensagens. Quando nenhum *nome do esquema* for fornecido, o padrão é o esquema padrão para o usuário atual.  
  
 *nome_da_fila*  
 O nome da fila da qual receber mensagens.  
  
 EM *table_variable*  
 Especifica a variável de tabela na qual a instrução RECEIVE coloca mensagens. A variável de tabela deve ter o mesmo número de colunas que as mensagens. O tipo de dados de cada coluna na variável de tabela deve poder ser convertido implicitamente no tipo de dados da coluna correspondente nas mensagens. Se INTO não estiver especificado, as mensagens serão retornadas como um conjunto de resultados.  
  
 WHERE  
 Especifica a conversa ou grupo de conversa das mensagens recebidas. Se omitido, as mensagens serão retornadas do próximo grupo de conversa disponível.  
  
 conversation_handle = *conversation_handle*  
 Especifica a conversa para mensagens recebidas. O *identificador de conversação* fornecido deve ser um **uniqueidentifer**, ou um tipo que pode ser convertido em **uniqueidentifier**.  
  
 conversation_group_id = *conversation_group_id*  
 Especifica o grupo de conversa das mensagens recebidas. O *ID de grupo de conversa é* fornecido deve ser um **uniqueidentifier**, ou um tipo conversível em **uniqueidentifier**.  
  
 Tempo limite *tempo limite*  
 Especifica o período de tempo, em milissegundos, durante o qual a instrução aguarda uma mensagem. Essa cláusula pode ser usada apenas com a cláusula WAITFOR. Se essa cláusula não for especificada, ou o tempo limite é -**1**, o tempo de espera é ilimitado. Se o tempo limite expirar, RECEIVE retornará um conjunto de resultados vazio.  
  
## <a name="remarks"></a>Comentários  
  
> [!IMPORTANT]  
>  Se a instrução RECEIVE não for a primeira instrução em um lote ou procedimento armazenado, a instrução anterior deverá ser encerrada com um ponto-e-vírgula (;).  
  
 A instrução RECEIVE lê mensagens de uma fila e retorna um conjunto de resultados. O conjunto de resultados consiste em zero ou mais linhas, cada uma das quais contêm uma mensagem. Se a cláusula INTO não for usada, e *column_specifier* não atribui valores a variáveis locais, a instrução retorna um conjunto de resultados para o programa de chamada.  
  
 As mensagens retornadas pela instrução RECEIVE podem ser de tipos de mensagem diferentes. Os aplicativos podem usar o **message_type_name** coluna para rotear cada mensagem para código que lida com o tipo de mensagem associado. Há duas classes de tipos de mensagem:  
  
-   Tipos de mensagem definidos pelo aplicativo que são criados com a instrução CREATE MESSAGE TYPE. O conjunto de tipos de mensagem definidos pelo aplicativo que são permitidos em uma conversa são definidos pelo contrato do [!INCLUDE[ssSB](../../includes/sssb-md.md)] especificado para a conversa.  
  
-   Mensagens do sistema [!INCLUDE[ssSB](../../includes/sssb-md.md)] que retornam informações de status ou de erro.  
  
 A instrução RECEIVE remove mensagens recebidas da fila a menos que a fila especifique retenção de mensagem. Quando a configuração de retenção para a fila for ON, a instrução RECEIVE atualizará o **status** coluna **0** e deixa as mensagens na fila. Quando uma transação que contém uma instrução RECEIVE é revertida, todas as alterações feitas na fila na transação também são revertidas, retornando mensagens para a fila.  
  
 Todas as mensagens retornadas por uma instrução RECEIVE pertencem ao mesmo grupo de conversa. A instrução RECEIVE bloqueia o grupo de conversa das mensagens retornadas até que a transação que contém a instrução termine. Uma instrução RECEIVE retorna mensagens que têm um **status** de **1.** O conjunto de resultados retornado por uma instrução RECEIVE é ordenado implicitamente:  
  
-   Se mensagens de vários grupos de conversa atenderem às condições da cláusula WHERE, a instrução RECEIVE retornará todas as mensagens de uma conversa antes de retornar mensagens para qualquer outra conversa. As conversas são processadas em ordem decrescente de nível de prioridade.  
  
-   Para uma determinada conversa, uma instrução RECEIVE retorna mensagens em crescente **message_sequence_number** ordem.  
  
 A cláusula WHERE da instrução RECEIVE só pode conter uma condição de pesquisa que usa o **conversation_handle** ou **conversation_group_id**. O critério de pesquisa não pode conter uma ou mais das outras colunas na fila. O **conversation_handle** ou **conversation_group_id** não pode ser uma expressão. O conjunto de mensagens retornado depende das condições especificadas na cláusula WHERE:  
  
-   Se **conversation_handle** for especificado, RECEIVE retornará todas as mensagens da conversa especificada que estão disponíveis na fila.  
  
-   Se **conversation_group_id** for especificado, RECEIVE retornará todas as mensagens que estão disponíveis na fila de qualquer conversa que seja membro do grupo de conversa especificado.  
  
-   Se não houver nenhuma cláusula WHERE, RECEIVE determinará qual grupo de conversa:  
  
    -   Tem uma ou mais mensagens na fila.  
  
    -   Não foi bloqueado por outra instrução RECEIVE.  
  
    -   Tem o nível de prioridade mais alto de todos os grupos de conversa que atendem a esses critérios.  
  
     Em seguida, RECEIVE retornará todas as mensagens disponíveis na fila de qualquer conversa membro do grupo de conversa selecionado.  
  
 Se o identificador de conversa ou de grupo de conversa especificado na cláusula WHERE não existir ou não estiver associado à fila especificada, a instrução RECEIVE retornará um erro.  
  
 Se a fila especificada na instrução RECEIVE tiver o status de fila definido como OFF, a instrução falhará com um erro [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Quando a cláusula WAITFOR está especificada, a instrução aguarda o tempo limite especificado ou até que um conjunto de resultados esteja disponível. Se a fila for descartada ou se o status da fila estiver definido como OFF enquanto a instrução estiver aguardando, a instrução retornará um erro imediatamente. Se a instrução RECEIVE especificar um grupo de conversa ou identificador de conversa e o serviço dessa conversa for descartado ou movido para outra fila, a instrução RECEIVE relatará um erro [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 RECEIVE não é válido em uma função definida pelo usuário.  
  
 A instrução RECEIVE não tem nenhuma prevenção de privação de prioridade. Se uma única instrução RECEIVE bloquear um grupo de conversa e recuperar muitas mensagens de conversa de baixa prioridade, nenhuma mensagem poderá ser recebida de conversas de alta prioridade no grupo. Para evitar isso, ao recuperar mensagens de conversas de baixa prioridade, use a cláusula TOP para limitar o número de mensagens recuperadas por cada instrução RECEIVE.  
  
## <a name="queue-columns"></a>Colunas de fila  
 A tabela a seguir lista as colunas em uma fila.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**status**|**tinyint**|Status da mensagem. Para mensagens retornadas pelo comando RECEIVE, o status é sempre **0**. Mensagens na fila podem conter um dos seguintes valores:<br /><br /> **0**= pronto**1**= recebeu mensagem**2**= ainda não concluída**3**= mensagem enviada retida|  
|**prioridade**|**tinyint**|O nível de prioridade de conversa aplicado à mensagem.|  
|**queuing_order**|**bigint**|Número da ordem da mensagem na fila.|  
|**conversation_group_id**|**uniqueidentifier**|O identificador do grupo de conversa a que pertence essa mensagem.|  
|**conversation_handle**|**uniqueidentifier**|Tratamento para a conversa da qual essa mensagem faz parte.|  
|**message_sequence_number**|**bigint**|Número de sequência da mensagem na conversa.|  
|**SERVICE_NAME**|**nvarchar(512)**|O nome do serviço a que se destina a conversa.|  
|**service_id**|**int**|Identificador de objeto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do serviço para o qual a conversa é destinada.|  
|**service_contract_name**|**nvarchar(256)**|O nome do contrato que a conversa segue.|  
|**service_contract_id**|**int**|Identificador de objeto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do contrato que a conversa segue.|  
|**message_type_name**|**nvarchar(256)**|O nome do tipo de mensagem que descreve o formato da mensagem. Mensagens podem ser do tipo de mensagem de aplicativo ou mensagens de sistema de Agente.|  
|**message_type_id**|**int**|Identificador de objeto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do tipo de mensagem que descreve a mensagem.|  
|**validação**|**nchar(2)**|Validação usada para a mensagem.<br /><br /> **E**= vazio**N**= None**X**= XML|  
|**message_body**|**varbinary (max)**|Conteúdo da mensagem.|  
  
## <a name="permissions"></a>Permissões  
 Para receber uma mensagem, o usuário atual deve ter permissão RECEIVE na fila.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-receiving-all-columns-for-all-messages-in-a-conversation-group"></a>A. Recebendo todas as colunas de todas as mensagens em um grupo de conversa  
 O exemplo a seguir recebe todas as mensagens disponíveis para o próximo grupo de conversa disponível da fila `ExpenseQueue`. A instrução retorna as mensagens como um conjunto de resultados.  
  
```  
RECEIVE * FROM ExpenseQueue ;  
```  
  
### <a name="b-receiving-specified-columns-for-all-messages-in-a-conversation-group"></a>B. Recebendo colunas especificadas de todas as mensagens em um grupo de conversa  
 O exemplo a seguir recebe todas as mensagens disponíveis para o próximo grupo de conversa disponível da fila `ExpenseQueue`. A instrução retorna as mensagens como um conjunto de resultados que contém as colunas `conversation_handle`, `message_type_name` e `message_body`.  
  
```  
RECEIVE conversation_handle, message_type_name, message_body  
FROM ExpenseQueue ;  
```  
  
### <a name="c-receiving-the-first-available-message-in-the-queue"></a>C. Recebendo a primeira mensagem disponível na fila  
 O exemplo a seguir recebe a primeira mensagem disponível da fila `ExpenseQueue` como um conjunto de resultados.  
  
```  
RECEIVE TOP (1) * FROM ExpenseQueue ;  
```  
  
### <a name="d-receiving-all-messages-for-a-specified-conversation"></a>D. Recebendo todas as mensagens para uma conversa especificada  
 O exemplo a seguir recebe todas as mensagens disponíveis para a conversa especificada da fila `ExpenseQueue` como um conjunto de resultados.  
  
```  
DECLARE @conversation_handle UNIQUEIDENTIFIER ;  
  
SET @conversation_handle = <retrieve conversation from database> ;  
  
RECEIVE *  
FROM ExpenseQueue  
WHERE conversation_handle = @conversation_handle ;  
```  
  
### <a name="e-receiving-messages-for-a-specified-conversation-group"></a>E. Recebendo mensagens para um grupo de conversa especificado  
 O exemplo a seguir recebe todas as mensagens disponíveis para o grupo de conversa especificado da fila `ExpenseQueue` como um conjunto de resultados.  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_group_id =   
    <retrieve conversation group ID from database> ;  
  
RECEIVE *  
FROM ExpenseQueue  
WHERE conversation_group_id = @conversation_group_id ;  
```  
  
### <a name="f-receiving-into-a-table-variable"></a>F. Recebendo em uma variável de tabela  
 O exemplo a seguir recebe todas as mensagens disponíveis para um grupo de conversa especificado da fila `ExpenseQueue` em uma variável de tabela.  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
DECLARE @procTable TABLE(  
     service_instance_id UNIQUEIDENTIFIER,  
     handle UNIQUEIDENTIFIER,  
     message_sequence_number BIGINT,  
     service_name NVARCHAR(512),  
     service_contract_name NVARCHAR(256),  
     message_type_name NVARCHAR(256),  
     validation NCHAR,  
     message_body VARBINARY(MAX)) ;  
  
SET @conversation_group_id = <retrieve conversation group ID from database> ;  
  
RECEIVE TOP (1)  
    conversation_group_id,  
    conversation_handle,  
    message_sequence_number,  
    service_name,  
    service_contract_name,  
    message_type_name,  
    validation,  
    message_body  
FROM ExpenseQueue  
INTO @procTable  
WHERE conversation_group_id = @conversation_group_id ;  
```  
  
### <a name="g-receiving-messages-and-waiting-indefinitely"></a>G. Recebendo mensagens e esperando indefinidamente  
 O exemplo a seguir recebe todas as mensagens disponíveis para o próximo grupo de conversa disponível na fila `ExpenseQueue`. A instrução aguardará até que pelo menos uma mensagem esteja disponível e retornará um conjunto de resultados que contém todas as colunas de mensagem.  
  
```  
WAITFOR (  
    RECEIVE *  
    FROM ExpenseQueue) ;  
```  
  
### <a name="h-receiving-messages-and-waiting-for-a-specified-interval"></a>H. Recebendo mensagens e aguardando por um intervalo especificado  
 O exemplo a seguir recebe todas as mensagens disponíveis para o próximo grupo de conversa disponível na fila `ExpenseQueue`. A instrução aguarda durante 60 segundos ou até que pelo menos uma mensagem esteja disponível, o que ocorrer primeiro. A instrução retornará um conjunto de resultados que contém todas as colunas de mensagem se pelo menos uma mensagem estiver disponível. Caso contrário, a instrução retornará um conjunto de resultados vazio.  
  
```  
WAITFOR (  
    RECEIVE *  
    FROM ExpenseQueue ),  
TIMEOUT 60000 ;  
```  
  
### <a name="i-receiving-messages-modifying-the-type-of-a-column"></a>I. Recebendo mensagens, modificando o tipo de uma coluna  
 O exemplo a seguir recebe todas as mensagens disponíveis para o próximo grupo de conversa disponível na fila `ExpenseQueue`. Quando o tipo de mensagem declara que a mensagem contém um documento XML, a instrução converte o corpo da mensagem em XML.  
  
```  
WAITFOR (  
    RECEIVE message_type_name,  
        CASE  
            WHEN validation = 'X' THEN CAST(message_body as XML)  
            ELSE NULL  
         END AS message_body   
         FROM ExpenseQueue ),  
TIMEOUT 60000 ;  
```  
  
### <a name="j-receiving-a-message-extracting-data-from-the-message-body-retrieving-conversation-state"></a>J. Recebendo uma mensagem, extraindo dados do corpo da mensagem, recuperando o estado da conversa  
 O exemplo a seguir recebe a próxima mensagem disponível para o próximo grupo de conversa disponível na fila `ExpenseQueue`. Quando a mensagem é do tipo `//Adventure-Works.com/Expenses/SubmitExpense`, a instrução extrai a ID do funcionário e uma lista de itens do corpo da mensagem. A instrução também recupera o estado da conversa da tabela `ConversationState`.  
  
```  
WAITFOR(  
    RECEIVE   
    TOP(1)  
      message_type_name,  
      COALESCE(  
           (SELECT TOP(1) ConversationState  
            FROM CurrentConversations AS cc  
            WHERE cc.ConversationHandle = conversation_handle),  
           'NEW')  
      AS ConversationState,  
      COALESCE(  
          (SELECT TOP(1) ErrorCount  
           FROM CurrentConversations AS cc  
           WHERE cc.ConversationHandle = conversation_handle),   
           0)  
      AS ConversationErrors,  
      CASE WHEN message_type_name = N'//Adventure-Works.com/Expenses/SubmitExpense'  
          THEN CAST(message_body AS XML).value(  
                'declare namespace rpt = "http://Adventure-Works.com/schemas/expenseReport"  
                   (/rpt:ExpenseReport/rpt:EmployeeID)[1]', 'nvarchar(20)')  
         ELSE NULL  
      END AS EmployeeID,  
      CASE WHEN message_type_name = N'//Adventure-Works.com/Expenses/SubmitExpense'  
          THEN CAST(message_body AS XML).query(  
                'declare namespace rpt = "http://Adventure-Works.com/schemas/expenseReport"   
                     /rpt:ExpenseReport/rpt:ItemDetail')  
          ELSE NULL  
      END AS ItemList  
    FROM ExpenseQueue   
), TIMEOUT 60000 ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [BEGIN DIALOG CONVERSATION &#40; Transact-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [BEGIN CONVERSATION TIMER &#40; Transact-SQL &#41;](../../t-sql/statements/begin-conversation-timer-transact-sql.md)   
 [Instrução END CONVERSATION &#40; Transact-SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [CRIAR contrato &#40; Transact-SQL &#41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [Criar tipo de mensagem &#40; Transact-SQL &#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [Enviar &#40; Transact-SQL &#41;](../../t-sql/statements/send-transact-sql.md)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [REMOVER fila &#40; Transact-SQL &#41;](../../t-sql/statements/drop-queue-transact-sql.md)  
  
  

