---
title: ALTERAR a prioridade do agente (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- ALTER_BROKER_TSQL
- ALTER BROKER PRIORITY
- ALTER BROKER
- ALTER_BROKER_PRIORITY_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ALTER BROKER PRIORITY statement
- ssbdiagnose
ms.assetid: 15fda1b2-e4dd-4f9d-935a-2e38926075b2
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7bd2cfd04ccc1de66fab7c518fdc31191955b24b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="alter-broker-priority-transact-sql"></a>ALTER BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de uma prioridade de conversa do [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER BROKER PRIORITY ConversationPriorityName  
FOR CONVERSATION  
{ SET ( [ CONTRACT_NAME = {ContractName | ANY } ]  
        [ [ , ] LOCAL_SERVICE_NAME = {LocalServiceName | ANY } ]  
        [ [ , ] REMOTE_SERVICE_NAME = {'RemoteServiceName' | ANY } ]  
        [ [ , ] PRIORITY_LEVEL = { PriorityValue | DEFAULT } ]  
              )  
}  
[;]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConversationPriorityName*  
 Especifica o nome da prioridade de conversa a ser alterado. O nome deve recorrer a uma prioridade de conversa no banco de dados atual.  
  
 SET  
 Especifica os critérios para determinar se a prioridade de conversa é aplicável a uma conversa. SET é necessário e deve conter pelo menos um critério: CONTRACT_NAME, LOCAL_SERVICE_NAME, REMOTE_SERVICE_NAME ou PRIORITY_LEVEL.  
  
 CONTRACT_NAME = {*ContractName* | **ANY**}  
 Especifica o nome de um contrato a ser usado como critério para determinar se a prioridade de conversa se aplica a uma conversa. *ContractName* é um [!INCLUDE[ssDE](../../includes/ssde-md.md)] identificador e deve especificar o nome de um contrato no banco de dados atual.  
  
 *ContractName*  
 Especifica que a prioridade de conversa pode ser aplicada somente em conversas onde a instrução BEGIN DIALOG iniciou a conversa especificada ON CONTRACT *ContractName*.  
  
 ANY  
 Especifica que a prioridade de conversa pode ser se aplicada em qualquer conversa, independentemente do contrato utilizado.  
  
 Se CONTRACT_NAME não for especificado, a propriedade de contrato da prioridade de conversa não será alterada.  
  
 LOCAL_SERVICE_NAME = {*LocalServiceName* | **ANY**}  
 Especifica o nome de um serviço a ser usado como critério para determinar se a prioridade de conversa é aplicável a um ponto de extremidade de conversa.  
  
 *LocalServiceName* é um [!INCLUDE[ssDE](../../includes/ssde-md.md)] identificador e deve especificar o nome de um serviço de banco de dados atual.  
  
 *LocalServiceName*  
 Especifica que a prioridade de conversa pode ser se aplicada a:  
  
-   Qualquer ponto de extremidade de conversa de iniciador cujo nome de serviço de iniciador corresponda *LocalServiceName*.  
  
-   Qualquer ponto de extremidade de conversa de destino cujo nome de serviço de destino corresponda *LocalServiceName*.  
  
 ANY  
 -   Especifica que a prioridade de conversa pode ser aplicada em qualquer ponto de extremidade de conversa, independentemente do nome do serviço local usado pelo ponto de extremidade.  
  
 Se LOCAL_SERVICE_NAME não for especificado, a propriedade de serviço local da prioridade de conversa não será alterada.  
  
 REMOTE_SERVICE_NAME = {'*RemoteServiceName*' | **ANY**}  
 Especifica o nome de um serviço a ser usado como critério para determinar se a prioridade de conversa é aplicável a um ponto de extremidade de conversa.  
  
 *RemoteServiceName* é um literal do tipo **nvarchar (256)**. [!INCLUDE[ssSB](../../includes/sssb-md.md)]usa uma comparação byte por byte para corresponder a *RemoteServiceName* cadeia de caracteres. A comparação diferencia maiúsculas de minúsculas e não considera o agrupamento atual. O serviço de destino pode estar na instância atual do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou em uma instância remota do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 '*RemoteServiceName*'  
 Especifica que a prioridade de conversa seja atribuída ao seguinte:  
  
-   Qualquer ponto de extremidade de conversa de iniciador cujo nome de serviço de destino associado corresponda *RemoteServiceName*.  
  
-   Qualquer ponto de extremidade de conversa de destino cujo nome de serviço de iniciador associado corresponda *RemoteServiceName*.  
  
 ANY  
 Especifica que a prioridade de conversa se aplica a qualquer ponto de extremidade de conversa, seja qual for o nome do serviço remoto associado ao ponto de extremidade.  
  
 Se REMOTE_SERVICE_NAME não for especificado, a propriedade de serviço remoto da prioridade de conversa não será alterada.  
  
 PRIORITY_LEVEL = { *PriorityValue* | **padrão** }  
 Especifica o nível de prioridade a ser atribuído a qualquer ponto de extremidade de conversa que use os contratos e serviços especificados na prioridade de conversa. *PriorityValue* deve ser um inteiro literal de 1 (prioridade mais baixa) a 10 (prioridade mais alta).  
  
 Se PRIORITY_LEVEL não for especificado, a propriedade do nível de prioridade da prioridade de conversa não será alterada.  
  
## <a name="remarks"></a>Comentários  
 Nenhuma propriedade alterada por ALTER BROKER PRIORITY se aplica a conversas existentes. As conversas existentes continuam com a prioridade que foi atribuída quando elas foram iniciadas.  
  
 Para obter mais informações, consulte [CREATE BROKER PRIORITY &#40; Transact-SQL &#41; ](../../t-sql/statements/create-broker-priority-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Permissão para criar uma prioridade de conversa assume como padrão membros do **db_ddladmin** ou **db_owner** funções de banco de dados fixas e o **sysadmin** função de servidor fixa. Requer a permissão ALTER no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-only-the-priority-level-of-an-existing-conversation-priority"></a>A. Alterando apenas o nível de prioridade de uma prioridade de conversa existente.  
 Altera o nível de prioridade, mas não altera o contrato, o serviço local ou as propriedades de serviço remoto.  
  
```  
ALTER BROKER PRIORITY SimpleContractDefaultPriority  
    FOR CONVERSATION  
    SET (PRIORITY_LEVEL = 3);  
```  
  
### <a name="b-changing-all-of-the-properties-of-an-existing-conversation-priority"></a>B. Alterando todas as propriedades de uma prioridade de conversa existente.  
 Altera o nível de prioridade, o contrato, o serviço local e as propriedades de serviço remoto.  
  
```  
ALTER BROKER PRIORITY SimpleContractPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContractB,  
         LOCAL_SERVICE_NAME = TargetServiceB,  
         REMOTE_SERVICE_NAME = N'InitiatorServiceB',  
         PRIORITY_LEVEL = 8);  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE BROKER PRIORITY &#40; Transact-SQL &#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [DROP BROKER PRIORITY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [conversation_priorities &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
