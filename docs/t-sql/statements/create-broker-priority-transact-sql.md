---
title: CRIAR a prioridade do agente (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- CREATE BROKER PRIORITY
- PRIORITY_TSQL
- CREATE_BROKER_PRIORITY_TSQL
- PRIORITY
- CREATE BROKER
- BROKER_TSQL
- BROKER
- CREATE_BROKER_TSQL
- BROKER PRIORITY
- BROKER_PRIORITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE BROKER PRIORITY statement
ms.assetid: e0bbebfa-b7c3-4825-8169-7281f7e6de98
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c7a1d85cba038eb3f7ef4a4e3198485943e8e194
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-broker-priority-transact-sql"></a>CREATE BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define um nível de prioridade e o conjunto de critérios para determinar quais conversas do [!INCLUDE[ssSB](../../includes/sssb-md.md)] devem ser atribuídas ao nível de prioridade. O nível de prioridade é atribuído a qualquer ponto de extremidade de conversa que usa a mesma combinação de contratos e serviços que são especificados na prioridade de conversa. As prioridades variam em valor, de 1 (baixa) a 10 (alta). O padrão é 5.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE BROKER PRIORITY ConversationPriorityName  
FOR CONVERSATION  
[ SET ( [ CONTRACT_NAME = {ContractName | ANY } ]  
        [ [ , ] LOCAL_SERVICE_NAME = {LocalServiceName | ANY } ]  
        [ [ , ] REMOTE_SERVICE_NAME = {'RemoteServiceName' | ANY } ]  
        [ [ , ] PRIORITY_LEVEL = {PriorityValue | DEFAULT } ]  
       )  
]  
[;]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConversationPriorityName*  
 Especifica o nome desta prioridade de conversa. O nome deve ser exclusivo no banco de dados atual e estar de acordo com as regras para [!INCLUDE[ssDE](../../includes/ssde-md.md)] [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 SET  
 Especifica os critérios para determinar se a prioridade de conversa é aplicável a uma conversa. Se for especificado, SET deve conter pelo menos um critério: CONTRACT_NAME, LOCAL_SERVICE_NAME, REMOTE_SERVICE_NAME ou PRIORITY_LEVEL. Se SET não for especificado, os padrões serão fixos para os três critérios.  
  
 CONTRACT_NAME = {*ContractName* | **ANY**}  
 Especifica o nome de um contrato a ser usado como critério para determinar se a prioridade de conversa se aplica a uma conversa. *ContractName* é um [!INCLUDE[ssDE](../../includes/ssde-md.md)] identificador e deve especificar o nome de um contrato no banco de dados atual.  
  
 *ContractName*  
 Especifica que a prioridade de conversa pode ser aplicada somente em conversas onde a instrução BEGIN DIALOG iniciou a conversa especificada ON CONTRACT *ContractName*.  
  
 ANY  
 Especifica que a prioridade de conversa pode ser se aplicada em qualquer conversa, independentemente do contrato utilizado.  
  
 O padrão é ANY.  
  
 LOCAL_SERVICE_NAME = {*LocalServiceName* | **ANY**}  
 Especifica o nome de um serviço a ser usado como critério para determinar se a prioridade de conversa é aplicável a um ponto de extremidade de conversa.  
  
 *LocalServiceName* é um [!INCLUDE[ssDE](../../includes/ssde-md.md)] identificador. Deve especificar o nome de um serviço no banco de dados atual.  
  
 *LocalServiceName*  
 Especifica que a prioridade de conversa pode ser se aplicada a:  
  
-   Qualquer ponto de extremidade de conversa de iniciador cujo nome de serviço de iniciador corresponda *LocalServiceName*.  
  
-   Qualquer ponto de extremidade de conversa de destino cujo nome de serviço de destino corresponda *LocalServiceName*.  
  
 ANY  
 -   Especifica que a prioridade de conversa pode ser aplicada em qualquer ponto de extremidade de conversa, independentemente do nome do serviço local usado pelo ponto de extremidade.  
  
 O padrão é ANY.  
  
 REMOTE_SERVICE_NAME = {'*RemoteServiceName*' | **ANY**}  
 Especifica o nome de um serviço a ser usado como critério para determinar se a prioridade de conversa é aplicável a um ponto de extremidade de conversa.  
  
 *RemoteServiceName* é um literal do tipo **nvarchar (256)**. [!INCLUDE[ssSB](../../includes/sssb-md.md)]usa uma comparação byte por byte para corresponder a *RemoteServiceName* cadeia de caracteres. A comparação diferencia maiúsculas de minúsculas e não considera o agrupamento atual. O serviço de destino pode estar na instância atual do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou em uma instância remota do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 '*RemoteServiceName*'  
 Especifica que a prioridade de conversa pode ser se aplicada a:  
  
-   Qualquer ponto de extremidade de conversa de iniciador cujo nome de serviço de destino associado corresponda *RemoteServiceName*.  
  
-   Qualquer ponto de extremidade de conversa de destino cujo nome de serviço de iniciador associado corresponda *RemoteServiceName*.  
  
 ANY  
 Especifica que a prioridade de conversa pode ser aplicada em qualquer ponto de extremidade de conversa, independentemente do nome do serviço remoto associado ao ponto de extremidade.  
  
 O padrão é ANY.  
  
 PRIORITY_LEVEL = { *PriorityValue* | **padrão** }  
 Especifica a prioridade a ser atribuída a qualquer ponto de extremidade da conversa que use os contratos e os serviços especificados na prioridade da conversa. *PriorityValue* deve ser um inteiro literal de 1 (prioridade mais baixa) a 10 (prioridade mais alta). O padrão é 5.  
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssSB](../../includes/sssb-md.md)] atribui níveis de prioridade a pontos de extremidade de conversa. Os níveis de prioridade controlam a prioridade das operações associadas ao ponto de extremidade. Cada conversa tem dois pontos de extremidade de conversa:  
  
-   O ponto de extremidade de conversa de iniciador associa um lado da conversa ao serviço iniciador e à fila do iniciador. O ponto de extremidade de conversa do iniciador é criado quando a instrução BEGIN DIALOG é executada. As operações associadas ao ponto de extremidade de conversa do iniciador incluem:  
  
    -   Envia a partir do serviço iniciador.  
  
    -   Recebe da fila do iniciador.  
  
    -   Obter o próximo grupo de conversa da fila de iniciador.  
  
-   O ponto de extremidade de conversa de destino associa o outro lado da conversa ao serviço de destino e à fila. O ponto de extremidade de conversa de destino é criado quando a conversa é usada para enviar uma mensagem à fila de destino. As operações associadas ao ponto de extremidade de conversa de destino incluem:  
  
    -   Recebe da fila de destino.  
  
    -   Envia do serviço de destino.  
  
    -   Obtendo o próximo grupo de conversa da fila de destino.  
  
 O [!INCLUDE[ssSB](../../includes/sssb-md.md)] atribui níveis de prioridade de conversa durante a criação de pontos de extremidade de conversa. O ponto de extremidade de conversa retém o nível de prioridade até que a conversa termine. As novas prioridades ou as alterações de prioridades existentes não se aplicam às conversas existentes.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]atribui o nível de prioridade de um ponto de extremidade de conversa da prioridade de conversa cujos critérios de serviços e contrato melhor correspondem às propriedades do ponto de extremidade. A tabela a seguir apresenta a precedência de correspondência:  
  
|Contrato de operação|Serviço local de operação|Serviço remoto de operação|  
|------------------------|-----------------------------|------------------------------|  
|*ContractName*|*LocalServiceName*|*RemoteServiceName*|  
|*ContractName*|*LocalServiceName*|ANY|  
|*ContractName*|ANY|*RemoteServiceName*|  
|*ContractName*|ANY|ANY|  
|ANY|*LocalServiceName*|*RemoteServiceName*|  
|ANY|*LocalServiceName*|ANY|  
|ANY|ANY|*RemoteServiceName*|  
|ANY|ANY|ANY|  
  
 O [!INCLUDE[ssSB](../../includes/sssb-md.md)] primeiro procura uma prioridade cujo contrato, serviço local e serviço remoto especificados correspondam aos usados pela operação. Se for encontrado algum, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] procura uma prioridade com contrato e serviço local que correspondam àqueles usados pela operação, na qual o serviço remoto esteja especificado como ANY. Isso continua com relação a todas as variações listadas na tabela de prioridades. Se não houver correspondência, a prioridade padrão de 5 será atribuída à operação.  
  
 O [!INCLUDE[ssSB](../../includes/sssb-md.md)] atribui um nível de prioridade independentemente a cada ponto de extremidade de conversa. Para que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] atribua níveis de prioridade aos pontos de extremidade de conversa iniciador e de destino, é preciso assegurar que os dois pontos estejam cobertos por prioridades de conversa. Se o iniciador e os pontos de extremidade de conversa de destino estiverem em bancos de dados separados, será necessário criar prioridades de conversa em todos os bancos de dados. O mesmo nível de prioridade é especificado, em geral, para os dois pontos de extremidade de conversa de uma conversa, mas é possível especificar níveis de prioridade diferentes.  
  
 Níveis de prioridade são sempre aplicados às operações que recebem mensagens ou identificadores de grupo de conversa de uma fila. Níveis de prioridade também são aplicados ao transmitir mensagens de uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para outra.  
  
 Níveis de prioridade não são usados ao transmitir mensagens:  
  
-   De um banco de dados onde a opção de banco de dados HONOR_BROKER_PRIORITY é definida como OFF. Para obter mais informações, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
-   Entre serviços na mesma instância do Mecanismo de Banco de Dados.  
  
-   Todos os [!INCLUDE[ssSB](../../includes/sssb-md.md)] operações em um banco de dados serão atribuídas prioridades padrão 5 se nenhuma prioridade de conversa tiver sido criada no banco de dados.  
  
## <a name="permissions"></a>Permissões  
 A permissão para criar uma prioridade de conversa assume como padrão os membros das funções de banco de dados fixas db_ddladmin ou db_owner e a função de servidor fixa sysadmin. Requer a permissão ALTER no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-assigning-a-priority-level-to-both-directions-of-a-conversation"></a>A. Atribuindo um nível de prioridade às duas direções de uma conversa.  
 Essas duas prioridades de conversa asseguram que a todas as operações que usam `SimpleContract` entre `TargetService` e `InitiatorAService` seja atribuído o nível de prioridade 3.  
  
```  
CREATE BROKER PRIORITY InitiatorAToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = InitiatorServiceA,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 3);  
CREATE BROKER PRIORITY TargetToInitiatorAPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'InitiatorServiceA',  
         PRIORITY_LEVEL = 3);  
```  
  
### <a name="b-setting-the-priority-level-for-all-conversations-that-use-a-contract"></a>B. Definindo o nível de prioridade para todas as conversas que usam um contrato  
 Atribui um nível de prioridade `7` a todas as operações que usam um contrato nomeado `SimpleContract`. Supõe-se que não há nenhuma outra prioridade que especifique `SimpleContract` e um serviço local ou remoto.  
  
```  
CREATE BROKER PRIORITY SimpleContractDefaultPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 7);  
```  
  
### <a name="c-setting-a-base-priority-level-for-a-database"></a>C. Definindo um nível de prioridade básico para um banco de dados.  
 Define prioridades de conversa para dois serviços específicos e, em seguida, defina uma prioridade de conversa que corresponderá a todos os outros pontos de extremidade de conversa. Isso não substitui a prioridade padrão, que é sempre 5, mas minimiza o número de itens atribuídos ao padrão.  
  
```  
CREATE BROKER PRIORITY [//Adventure-Works.com/Expenses/ClaimPriority]  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = ANY,  
         LOCAL_SERVICE_NAME = //Adventure-Works.com/Expenses/ClaimService,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 9);  
CREATE BROKER PRIORITY [//Adventure-Works.com/Expenses/ApprovalPriority]  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = ANY,  
         LOCAL_SERVICE_NAME = //Adventure-Works.com/Expenses/ClaimService,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY [//Adventure-Works.com/Expenses/BasePriority]  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = ANY,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 3);  
```  
  
### <a name="d-creating-three-priority-levels-for-a-target-service-by-using-services"></a>D. Criando três níveis de prioridade para um serviço de destino com o uso de serviços  
 Oferece suporte a um sistema que fornece três níveis de desempenho: Ouro (alto), Prata (meio) e Bronze (baixo). Há um contrato, mas cada nível tem um serviço iniciador separado. Todos os serviços de iniciador se comunicam com um serviço de destino central.  
  
```  
CREATE BROKER PRIORITY GoldInitToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = GoldInitiatorService,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY GoldTargetToInitPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'GoldInitiatorService',  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY SilverInitToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = SilverInitiatorService,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 4);  
CREATE BROKER PRIORITY SilverTargetToInitPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'SilverInitiatorService',  
         PRIORITY_LEVEL = 4);  
CREATE BROKER PRIORITY BronzeInitToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = BronzeInitiatorService,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 2);  
CREATE BROKER PRIORITY BronzeTargetToInitPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'BronzeInitiatorService',  
         PRIORITY_LEVEL = 2);  
```  
  
### <a name="e-creating-three-priority-levels-for-multiple-services-using-contracts"></a>E. Criando três níveis de prioridade para vários serviços com o uso de contratos  
 Oferece suporte a um sistema que fornece três níveis de desempenho: Ouro (alto), Prata (meio) e Bronze (baixo). Cada nível tem um contrato separado. Estas prioridades se aplicam a qualquer serviço mencionado por conversas que usam os contratos.  
  
```  
CREATE BROKER PRIORITY GoldPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = GoldContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY SilverPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SilverContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 4);  
CREATE BROKER PRIORITY BronzePriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = BronzeContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 2);  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER BROKER PRIORITY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [BEGIN DIALOG CONVERSATION &#40; Transact-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [CRIAR contrato &#40; Transact-SQL &#41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP BROKER PRIORITY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [OBTER grupo de conversação &#40; Transact-SQL &#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [RECEBER &#40; Transact-SQL &#41;](../../t-sql/statements/receive-transact-sql.md)   
 [Enviar &#40; Transact-SQL &#41;](../../t-sql/statements/send-transact-sql.md)   
 [conversation_priorities &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  

