---
title: "ALTERAR a sessão de evento (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/07/2017
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
- ALTER EVENT SESSION
- ALTER_EVENT_SESSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- extended events [SQL Server], Transact-SQL
- ALTER EVENT SESSION statement
ms.assetid: da006ac9-f914-4995-a2fb-25b5d971cd90
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b6fd062bf55bb2630c436d452d2bab05a2f2d53d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-event-session-transact-sql"></a>ALTER EVENT SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia ou interrompe uma sessão de evento ou altera uma configuração de sessão de evento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER EVENT SESSION event_session_name  
ON SERVER  
{  
    [ [ {  <add_drop_event> [ ,...n] }     
       | { <add_drop_event_target> [ ,...n ] } ]   
    [ WITH ( <event_session_options> [ ,...n ] ) ]  
    ]  
    | [ STATE = { START | STOP } ]  
}  
  
<add_drop_event>::=  
{  
    [ ADD EVENT <event_specifier>   
         [ ( {   
                 [ SET { event_customizable_attribute = <value> [ ,...n ] } ]  
                 [ ACTION ( { [event_module_guid].event_package_name.action_name [ ,...n ] } ) ]  
                 [ WHERE <predicate_expression> ]  
        } ) ]  
   ]   
   | DROP EVENT <event_specifier> }  
  
<event_specifier> ::=  
{  
[event_module_guid].event_package_name.event_name  
}  
  
<predicate_expression> ::=   
{  
    [ NOT ] <predicate_factor> | {( <predicate_expression> ) }   
    [ { AND | OR } [ NOT ] { <predicate_factor> | ( <predicate_expression> ) } ]   
    [ ,...n ]  
}  
  
<predicate_factor>::=   
{  
    <predicate_leaf> | ( <predicate_expression> )  
}  
  
<predicate_leaf>::=  
{  
      <predicate_source_declaration> { = | < > | ! = | > | > = | < | < = } <value>   
    | [event_module_guid].event_package_name.predicate_compare_name ( <predicate_source_declaration>, <value> )   
}  
  
<predicate_source_declaration>::=   
{  
    event_field_name | ( [event_module_guid].event_package_name.predicate_source_name )  
}  
  
<value>::=   
{  
    number | 'string'  
}  
  
<add_drop_event_target>::=  
{  
    ADD TARGET <event_target_specifier>  
        [ ( SET { target_parameter_name = <value> [ ,...n] } ) ]  
    | DROP TARGET <event_target_specifier>  
}  
  
<event_target_specifier>::=  
{  
    [event_module_guid].event_package_name.target_name  
}  
  
<event_session_options>::=  
{  
    [    MAX_MEMORY = size [ KB | MB] ]  
    [ [,] EVENT_RETENTION_MODE = { ALLOW_SINGLE_EVENT_LOSS | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } ]  
    [ [,] MAX_DISPATCH_LATENCY = { seconds SECONDS | INFINITE } ]  
    [ [,] MAX_EVENT_SIZE = size [ KB | MB ] ]  
    [ [,] MEMORY_PARTITION_MODE = { NONE | PER_NODE | PER_CPU } ]  
    [ [,] TRACK_CAUSALITY = { ON | OFF } ]  
    [ [,] STARTUP_STATE = { ON | OFF } ]  
}  
```  
  
## <a name="arguments"></a>Argumentos  
  
|||  
|-|-|  
|Termo|Definição|  
|*event_session_name*|É o nome de uma sessão de evento existente.|  
|ESTADO = INÍCIO &#124; PARAR|Inicia ou para a sessão de evento. Este argumento é válido somente quando ALTER EVENT SESSION é aplicado a um objeto de sessão de evento.|  
|Adicionar evento \<event_specifier >|Associa o evento identificado por \<event_specifier > com a sessão de evento.|
|[*event_module_guid*]*. event_package_name.event_name*|É o nome de um evento em um pacote de evento, onde:<br /><br /> -   *event_module_guid* é o GUID para o módulo que contém o evento.<br />-   *event_package_name* é o pacote que contém o objeto de ação.<br />-   *event_name* é o objeto de evento.<br /><br /> Eventos aparecem na exibição sys.dm_xe_objects como object_type “evento”.|  
|DEFINIR { *event_customizable_attribute*= \<valor > [,... *n*] }|Especifica atributos personalizáveis do evento. Atributos personalizáveis aparecem na exibição sys.DM xe_object_columns como column_type "personalizável" e object_name = *event_name*.|  
|AÇÃO ({[*event_module_guid*]*. event_package_name.action_name* [ **,**... *n*] } )|É a ação a ser associada à sessão de evento, onde:<br /><br /> -   *event_module_guid* é o GUID para o módulo que contém o evento.<br />-   *event_package_name* é o pacote que contém o objeto de ação.<br />-   *action_name* é o objeto de ação.<br /><br /> Ações aparecem na exibição sys.dm_xe_objects como object_type “ação”.|  
|ONDE \<predicate_expression >|Especifica a expressão de predicado usada para determinar se um evento deve ser processado. Se \<predicate_expression > for true, o evento é processado mais pelas ações e destinos da sessão. Se \<predicate_expression > for false, o evento será descartado pela sessão antes de ser processada pelas ações e destinos para a sessão. As expressões de predicado são limitadas a 3.000 caracteres, o que limita os argumentos de cadeia de caracteres.|
|*event_field_name*|É o nome do campo de evento que identifica a origem do predicado.|  
|[event_module_guid].event_package_name.predicate_source_name|É o nome da origem do predicado global onde:<br /><br /> -   *event_module_guid* é o GUID para o módulo que contém o evento.<br />-   *event_package_name* é o pacote que contém o objeto de predicado.<br />-   *predicate_source_name* é definido na exibição sys.DM xe_objects como object_type 'pred_source'.|  
|[*event_module_guid*]. *event_package_name*. *predicate_compare_name*|É o nome do objeto de predicado a ser associado à sessão de evento, onde:<br /><br /> -   *event_module_guid* é o GUID para o módulo que contém o evento.<br />-   *event_package_name* é o pacote que contém o objeto de predicado.<br />-   *predicate_compare_name* é uma origem global definida na exibição sys.DM xe_objects como object_type "pred_compare".|  
|DROP EVENT \<event_specifier >|Descarta o evento identificado por  *\<event_specifier >*. \<event_specifier > deve ser válido na sessão de evento.|  
|Adicionar um destino \<event_target_specifier >|Associa o destino identificado por \<event_target_specifier > com a sessão de evento.|
|[*event_module_guid*]. *event_package_name*. *target_name*|É o nome do destino na sessão de evento, onde:<br /><br /> -   *event_module_guid* é o GUID para o módulo que contém o evento.<br />-   *event_package_name* é o pacote que contém o objeto de ação.<br />-   *target_name* é a ação. As ações aparecem na exibição sys.dm_xe_objects como object_type “destino”.|  
|DEFINIR { *target_parameter_name*= \<valor > [,... *n*] }|Define um parâmetro de destino. Parâmetros de destino aparecem na exibição sys.DM xe_object_columns como column_type "personalizável" e object_name = *target_name*.<br /><br /> **OBSERVAÇÃO!** Se você estiver usando o destino de buffer de anel, é recomendável que você defina o parâmetro de destino max_memory como 2048 KB (Quilobytes) para ajudar a evitar o truncamento de dados de saída XML. Para obter mais informações sobre quando usar os diferentes tipos de destino, consulte [SQL Server Extended Events Targets](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384).|  
|DESTINO de SOLTAR \<event_target_specifier >|Descarta o destino identificado por \<event_target_specifier >. \<event_target_specifier > deve ser válido na sessão de evento.|  
|EVENT_RETENTION_MODE = { **ALLOW_SINGLE_EVENT_LOSS** &#124; ALLOW_MULTIPLE_EVENT_LOSS &#124; NO_EVENT_LOSS}|Especifica o modo de retenção do evento para usar em tratamento de perda de evento.<br /><br /> **ALLOW_SINGLE_EVENT_LOSS**<br /> Um evento pode ser perdido da sessão. Um único evento será descartado somente quando todos os buffers de evento estiverem cheios. A perda de um único evento quando os buffers de evento estão cheios permite características de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceitáveis, enquanto minimiza a perda de dados no fluxo de evento processado.<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS<br /> Buffers de evento cheios que contêm vários eventos podem ser perdidos da sessão. O número de eventos perdidos depende do tamanho de memória alocado à sessão, do particionamento da memória e do tamanho dos eventos no buffer. Essa opção minimiza o impacto do desempenho no servidor quando buffers de evento são rapidamente enchidos, mas grandes números de eventos podem ser perdidos da sessão.<br /><br /> NO_EVENT_LOSS<br /> Nenhuma perda de evento é permitida. Essa opção assegura que todos os eventos gerados sejam retidos. O uso dessa opção força todas as tarefas que acionam eventos a esperar até que haja espaço disponível em um buffer de evento. Isso pode causar problemas de desempenho detectáveis enquanto a sessão de evento está ativa. As conexões de usuário poderão parar enquanto esperam a liberação de eventos do buffer.|  
|MAX_DISPATCH_LATENCY = { *segundos* segundos &#124; **Infinito** }|Especifica a quantidade de tempo em que os eventos serão colocados no buffer de memória antes que sejam despachados para destinos de sessão de evento. O valor mínimo de latência é 1 segundo. No entanto, o valor 0 pode ser usado para especificar a latência INFINITE. Por padrão, este valor é definido como 30 segundos.<br /><br /> *segundos* segundos<br /> O tempo, em segundos, a esperar antes de liberar buffers para os destinos. *segundos* é um número inteiro.<br /><br /> **INFINITO**<br /> Libera buffers para os destinos somente quando eles estão cheios ou quando a sessão de evento é fechada.<br /><br /> **OBSERVAÇÃO!** MAX_DISPATCH_LATENCY = 0 SECONDS é equivalente a MAX_DISPATCH_LATENCY = INFINITE.|  
|MAX_EVENT_SIZE =*tamanho* [KB &#124; **MB** ]|Especifica o tamanho máximo permitido para eventos. MAX_EVENT_SIZE deverá ser definido apenas para permitir eventos únicos maiores que MAX_MEMORY; sua definição como menos que MAX_MEMORY irá gerar um erro. *tamanho* é um número inteiro e pode ser um kilobyte (KB) ou um valor de megabytes (MB). Se *tamanho* é especificado em kilobytes, o tamanho mínimo permitido é de 64 KB. Quando MAX_EVENT_SIZE é definido, dois buffers de *tamanho* são à max_memory. Isso significa que a memória total usada para buffer de evento é MAX_MEMORY + 2 * MAX_EVENT_SIZE.|  
|MEMORY_PARTITION_MODE = { **NONE** &#124; PER_NODE &#124; PER_CPU}|Especifica o local onde buffers de evento são criados.<br /><br /> **NONE**<br /> Um único conjunto de buffers é criado dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.<br /><br /> POR nó - um conjunto de buffers é criado para cada nó NUMA.<br /><br /> POR CPU - um conjunto de buffers é criado para cada CPU.|  
|TRACK_CAUSALITY = {ON &#124; **OFF** }|Especifica se a causalidade deve ou não ser controlada. Se habilitada, a causalidade permitirá que eventos relacionados em conexões de servidor diferentes sejam correlacionados.|  
|STARTUP_STATE = {ON &#124; **OFF** }|Especifica se essa sessão de evento deve ser iniciada automaticamente quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicia.<br /><br /> Se STARTUP_STATE = ON a sessão de evento somente iniciará se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é interrompido e reiniciado.<br /><br /> NO = evento de sessão é iniciada na inicialização.<br /><br /> **DESATIVAR** = evento de sessão não foi iniciada na inicialização.|  
  
## <a name="remarks"></a>Comentários  
 Não podem ser usados os argumentos ADD e DROP na mesma instrução.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão ALTER ANY EVENT SESSION.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir inicia uma sessão de evento, obtém algumas estatísticas de sessão ao vivo e, em seguida, adiciona dois eventos à sessão existente.  
  
```  
-- Start the event session  
ALTER EVENT SESSION test_session  
ON SERVER  
STATE = start;  
GO  
-- Obtain live session statistics   
SELECT * FROM sys.dm_xe_sessions;  
SELECT * FROM sys.dm_xe_session_events;  
GO  
  
-- Add new events to the session  
ALTER EVENT SESSION test_session ON SERVER  
ADD EVENT sqlserver.database_transaction_begin,  
ADD EVENT sqlserver.database_transaction_end;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [Destinos de eventos estendidos do SQL Server](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)   
 [server_event_sessions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)   
 [xe_objects &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)   
 [sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)  
  
  

