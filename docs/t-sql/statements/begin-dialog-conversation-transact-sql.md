---
title: BEGIN DIALOG CONVERSATION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DIALOG CONVERSATION
- DIALOG
- BEGIN_DIALOG_TSQL
- BEGIN_DIALOG_CONVERSATION_TSQL
- DIALOG_CONVERSATION_TSQL
- DIALOG_TSQL
- BEGIN DIALOG
- BEGIN DIALOG CONVERSATION
dev_langs: TSQL
helpviewer_keywords:
- conversations [Service Broker]
- beginning dialogs
- dialogs [Service Broker], beginning
- BEGIN DIALOG CONVERSATION statement
- cryptography [SQL Server], conversations
- opening conversations
- encryption [SQL Server], conversations
- starting conversations
ms.assetid: 8e814f9d-77c1-4906-b8e4-668a86fc94ba
caps.latest.revision: "47"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a2ece31010207b6044504f099c11443a2fec0fa2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="begin-dialog-conversation-transact-sql"></a>BEGIN DIALOG CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia uma caixa de diálogo de um serviço para outro. Uma caixa de diálogo é uma conversa que fornece mensagens exatamente na mesma ordem entre dois serviços.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BEGIN DIALOG [ CONVERSATION ] @dialog_handle  
   FROM SERVICE initiator_service_name  
   TO SERVICE 'target_service_name'  
       [ , { 'service_broker_guid' | 'CURRENT DATABASE' }]   
   [ ON CONTRACT contract_name ]  
   [ WITH  
   [  { RELATED_CONVERSATION = related_conversation_handle   
      | RELATED_CONVERSATION_GROUP = related_conversation_group_id } ]   
   [ [ , ] LIFETIME = dialog_lifetime ]   
   [ [ , ] ENCRYPTION = { ON | OFF }  ] ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **@** *dialog_handle*  
 É uma variável usada para armazenar o identificador da caixa de diálogo gerada pelo sistema para a nova caixa de diálogo que é retornada pela instrução BEGIN DIALOG CONVERSATION. A variável deve ser do tipo **uniqueidentifier**.  
  
 DO serviço *initiator_service_name*  
 Especifica o serviço que inicia a caixa de diálogo. O nome especificado deve ser o nome de um serviço no banco de dados atual. A fila especificada para o serviço iniciador recebe mensagens retornadas pelo serviço de destino e mensagens criadas pelo Service Broker para essa conversa.  
  
 SERVIÇO **'***target_service_name***'**  
 Especifica o serviço de destino com o qual iniciar a caixa de diálogo. O *target_service_name* é do tipo **nvarchar (256)**. [!INCLUDE[ssSB](../../includes/sssb-md.md)]usa uma comparação byte por byte para corresponder a *target_service_name* cadeia de caracteres. Em outras palavras, a comparação diferencia maiúsculas de minúsculas e não leva em conta o agrupamento atual.  
  
 *service_broker_guid*  
 Especifica o banco de dados que hospeda o serviço de destino. Quando mais de um banco de dados hospeda uma instância do serviço de destino, você pode se comunicar com um banco de dados específico, fornecendo um *service_broker_guid*.  
  
 O *service_broker_guid* é do tipo **nvarchar (128)**. Para localizar o *service_broker_guid* para um banco de dados, execute a seguinte consulta no banco de dados:  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID() ;  
```  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 **'**BANCO DE DADOS ATUAL**'**  
 Especifica que a conversa usa o *service_broker_guid* para o banco de dados atual.  
  
 ON CONTRACT *contract_name*  
 Especifica o contrato que essa conversa segue. O contrato deve existir no banco de dados atual. Se o serviço de destino não aceitar novas conversas no contrato especificado, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] retornará uma mensagem de erro na conversa. Quando esta cláusula é omitida, a conversa segue o contrato denominado **padrão**.  
  
 RELATED_CONVERSATION **=***related_conversation_handle*  
 Especifica o grupo de conversa existente ao qual a nova caixa de diálogo é adicionada. Quando esta cláusula estiver presente, a caixa de diálogo Novo pertence ao mesmo grupo de conversa como o diálogo especificado por *related_conversation_handle*. O *related_conversation_handle*devem ser do tipo implicitamente conversível para o tipo **uniqueidentifier**. A instrução falhará se o *related_conversation_handle* não faz referência a uma caixa de diálogo existente.  
  
 RELATED_CONVERSATION_GROUP **= * related_conversation_group_id*  
 Especifica o grupo de conversa existente ao qual a nova caixa de diálogo é adicionada. Quando esta cláusula estiver presente, a caixa de diálogo Novo será adicionada ao grupo de conversa especificado por *related_conversation_group_id*. O *related_conversation_group_id*devem ser do tipo implicitamente conversível para o tipo **uniqueidentifier**. Se *related_conversation_group_id*referência um grupo de conversa existente, o service broker cria um novo grupo de conversa com especificado *related_conversation_group_id* e se relaciona a caixa de diálogo Novo a esse grupo de conversa.  
  
 Tempo de vida **= * dialog_lifetime*  
 Especifica o limite máximo de tempo que a caixa de diálogo permanecerá aberta. Para a caixa de diálogo ser concluída com êxito, os pontos de extremidade devem finalizar explicitamente a caixa de diálogo antes que seu tempo de vida expire. O *dialog_lifetime* valor deve ser expresso em segundos. Tempo de vida é do tipo **int**. Quando nenhuma cláusula LIFETIME é especificada, o tempo de vida da caixa de diálogo é o valor máximo de **int** tipo de dados.  
  
 ENCRYPTION  
 Especifica se as mensagens enviadas e recebidas nessa caixa de diálogo devem ser criptografadas quando forem enviadas para fora de uma instância de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uma caixa de diálogo que deve ser criptografada é uma *caixa de diálogo protegida*. Quando ENCRYPTION = ON e os certificados necessários para oferecer suporte à criptografia não estão configurados, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] retorna uma mensagem de erro na conversa. Se ENCRYPTION = OFF, criptografia será usada se uma associação de serviço remoto estiver configurada para o *target_service_name*; caso contrário, as mensagens são enviadas descriptografadas. Se esta cláusula não estiver presente, o valor padrão será ON.  
  
> [!NOTE]  
>  As mensagens trocadas com serviços na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nunca são criptografadas. Entretanto, uma chave de banco de dados mestre e os certificados para a criptografia ainda serão necessários para as conversas que usam criptografia se os serviços para a conversa estiverem em bancos de dados diferentes. Isso permite que as conversas continuem caso um dos bancos de dados seja movido para uma instância enquanto a conversa estiver em andamento.  
  
## <a name="remarks"></a>Remarks  
 Todas as mensagens fazem parte de uma conversa. Portanto, um serviço iniciador deve começar uma conversa com o serviço de destino antes de enviar-lhe uma mensagem. As informações especificadas na instrução BEGIN DIALOG CONVERSATION são semelhantes ao endereço em uma carta; o [!INCLUDE[ssSB](../../includes/sssb-md.md)] usa as informações para entregar as mensagens ao serviço correto. O serviço especificado na cláusula TO SERVICE é o endereço para o qual as mensagens são enviadas. O serviço especificado na cláusula FROM SERVICE é o endereço de retorno usado para mensagens de resposta.  
  
 O destino de uma conversa não precisa chamar BEGIN DIALOG CONVERSATION. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] cria uma conversa no banco de dados de destino quando a primeira mensagem da conversa chega do iniciador.  
  
 O início de uma caixa de diálogo cria um ponto de extremidade de conversa no banco de dados para o serviço iniciador, mas não cria uma conexão de rede à instância que hospeda o serviço de destino. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] não estabelece comunicação com o destino da caixa de diálogo até que a primeira mensagem seja enviada.  
  
 Quando a instrução BEGIN DIALOG CONVERSATION não especifica uma conversa relacionada ou um grupo de conversa relacionado, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] cria um novo grupo de conversa para a nova conversa.  
  
 O [!INCLUDE[ssSB](../../includes/sssb-md.md)] não permite agrupamentos arbitrários de conversas. Todas as conversas em um grupo de conversa devem ter o serviço especificado na cláusula FROM como o iniciador ou o destino da conversa.  
  
 O comando BEGIN DIALOG CONVERSATION bloqueia o grupo de conversa que contém o *dialog_handle* retornado. Quando o comando inclui uma cláusula RELATED_CONVERSATION_GROUP, o grupo de conversa para *dialog_handle* é o grupo de conversa especificado no *related_conversation_group_id* parâmetro. Quando o comando inclui uma cláusula RELATED_CONVERSATION, o grupo de conversa para *dialog_handle* o grupo de conversa é associado a *related_conversation_handle* especificado.  
  
 BEGIN DIALOG CONVERSATION não é válido em uma função definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Para iniciar uma caixa de diálogo, o usuário atual deve ter a permissão RECEIVE na fila para o serviço especificado na cláusula FROM do comando e a permissão REFERENCES para o contrato especificado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-beginning-a-dialog"></a>A. Iniciando uma caixa de diálogo  
 O exemplo a seguir inicia uma conversa de caixa de diálogo e armazena um identificador para a caixa de diálogo no `@dialog_handle.` O serviço `//Adventure-Works.com/ExpenseClient` é o iniciador e o serviço `//Adventure-Works.com/Expenses` é o destino da caixa de diálogo. A caixa de diálogo segue o contrato `//Adventure-Works.com/Expenses/ExpenseSubmission`.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
### <a name="b-beginning-a-dialog-with-an-explicit-lifetime"></a>B. Iniciando uma caixa de diálogo com um tempo de vida explícito  
 O exemplo a seguir inicia uma conversa de caixa de diálogo e armazena um identificador para a caixa de diálogo em `@dialog_handle`. O serviço `//Adventure-Works.com/ExpenseClient` é o iniciador da caixa de diálogo e o serviço `//Adventure-Works.com/Expenses` é o destino da caixa de diálogo. A caixa de diálogo segue o contrato `//Adventure-Works.com/Expenses/ExpenseSubmission`. Se a caixa de diálogo não for fechada pelo comando END CONVERSATION em `60` segundos, o agente a encerrará com um erro.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH LIFETIME = 60 ;  
```  
  
### <a name="c-beginning-a-dialog-with-a-specific-broker-instance"></a>C. Iniciando uma caixa de diálogo com uma instância de agente específica  
 O exemplo a seguir inicia uma conversa de caixa de diálogo e armazena um identificador para a caixa de diálogo em `@dialog_handle`. O serviço `//Adventure-Works.com/ExpenseClient` é o iniciador da caixa de diálogo e o serviço `//Adventure-Works.com/Expenses` é o destino da caixa de diálogo. A caixa de diálogo segue o contrato `//Adventure-Works.com/Expenses/ExpenseSubmission`. O agente roteia as mensagens dessa caixa de diálogo para o agente identificado pelo GUID `a326e034-d4cf-4e8b-8d98-4d7e1926c904.`  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses',   
              'a326e034-d4cf-4e8b-8d98-4d7e1926c904'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
### <a name="d-beginning-a-dialog-and-relating-it-to-an-existing-conversation-group"></a>D. Iniciando uma caixa de diálogo e relacionando-a com um grupo de conversa existente  
 O exemplo a seguir inicia uma conversa de caixa de diálogo e armazena um identificador para a caixa de diálogo em `@dialog_handle`. O serviço `//Adventure-Works.com/ExpenseClient` é o iniciador da caixa de diálogo e o serviço `//Adventure-Works.com/Expenses` é o destino da caixa de diálogo. A caixa de diálogo segue o contrato `//Adventure-Works.com/Expenses/ExpenseSubmission`. O agente associa a caixa de diálogo ao grupo de conversa identificado através do `@conversation_group_id` em vez de criar um novo grupo de conversa.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_group_id = <retrieve conversation group ID from database>  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH RELATED_CONVERSATION_GROUP = @conversation_group_id ;  
```  
  
### <a name="e-beginning-a-dialog-with-an-explicit-lifetime-and-relating-the-dialog-to-an-existing-conversation"></a>E. Iniciando uma caixa de diálogo com um tempo de vida explícito e relacionando-a a uma conversa existente  
 O exemplo a seguir inicia uma conversa de caixa de diálogo e armazena um identificador para a caixa de diálogo em `@dialog_handle`. O serviço `//Adventure-Works.com/ExpenseClient` é o iniciador da caixa de diálogo e o serviço `//Adventure-Works.com/Expenses` é o destino da caixa de diálogo. A caixa de diálogo segue o contrato `//Adventure-Works.com/Expenses/ExpenseSubmission`. A nova caixa de diálogo pertence ao mesmo grupo de conversa ao qual `@existing_conversation_handle` pertence. Se a caixa de diálogo não for fechada pelo comando END CONVERSATION em `600` segundos, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] a encerrará com um erro.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER  
DECLARE @existing_conversation_handle UNIQUEIDENTIFIER  
  
SET @existing_conversation_handle = <retrieve conversation handle from database>  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH RELATED_CONVERSATION = @existing_conversation_handle  
   LIFETIME = 600 ;  
```  
  
### <a name="f-beginning-a-dialog-with-optional-encryption"></a>F. Iniciando uma caixa de diálogo com criptografia opcional  
 O exemplo a seguir inicia uma caixa de diálogo e armazena um identificador para ela em `@dialog_handle`. O serviço `//Adventure-Works.com/ExpenseClient` é o iniciador da caixa de diálogo e o serviço `//Adventure-Works.com/Expenses` é o destino da caixa de diálogo. A caixa de diálogo segue o contrato `//Adventure-Works.com/Expenses/ExpenseSubmission`. A conversa neste exemplo permite que a mensagem passe pela rede sem criptografia se ela não estiver disponível.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH ENCRYPTION = OFF ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [BEGIN CONVERSATION TIMER &#40;Transact-SQL&#41;](../../t-sql/statements/begin-conversation-timer-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [MOVE CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/move-conversation-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
