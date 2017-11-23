---
title: sp_configure_peerconflictdetection (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_configure_peerconflictdetection_TSQL
- sp_configure_peerconflictdetection
helpviewer_keywords: sp_configure_peerconflictdetection
ms.assetid: 45117cb2-3247-433f-ba3d-7fa19514b1c3
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1fed4cb47795554df26deb08f496edba86b5a4d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spconfigurepeerconflictdetection-transact-sql"></a>sp_configure_peerconflictdetection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Configura a detecção de conflitos para uma publicação envolvida em uma topologia de replicação transacional ponto a ponto. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md). Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_configure_peerconflictdetection [ @publication = ] 'publication'  
    [ , [ @action = ] 'action']  
    [ , [ @originator_id = ] originator_id ]  
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @continue_onconflict = ] 'continue_onconflict']  
    [ , [ @local = ] 'local']  
    [ , [ @timeout = ] timeout ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @publication=] '*publicação*'  
 É o nome da publicação para a qual configurar detecção de conflitos. *publicação* é **sysname**, sem padrão.  
  
 [ @action=] '*ação*'  
 Especifica se deve habilitar ou desabilitar a detecção de conflito para uma publicação. *ação* é **nvarchar (5)**, e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Habilitar**|Habilita a detecção de conflitos para uma publicação.|  
|**desabilitar**|Desabilita a detecção de conflitos para uma publicação.|  
|NULL (padrão)||  
  
 [ @originator_id=] *originator_id*  
 Especifica uma ID para um nó em uma topologia ponto a ponto. *originator_id* é **int**, com um padrão NULL. Essa ID é usada para detecção de conflitos se *ação* é definido como **habilitar**. Especifique uma ID positiva, diferente de zero, que nunca foi usada na topologia. Para uma lista de IDs que já foram usadas, consulte a tabela do sistema [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) .  
  
 [ @conflict_retention=] *conflict_retention*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @continue_onconflict=] '*continue_onconflict*']  
 Determina se o Agente de Distribuição deve continuar processando alterações depois da detecção de um conflito. *continue_onconflict* é **nvarchar (5)** com um valor padrão de FALSE.  
  
> [!CAUTION]  
>  Recomendamos que você use o valor padrão de FALSE. Quando essa opção é definida como TRUE, o Distribution Agent tenta convergir os dados na topologia aplicando a linha conflitante do nó que tem a ID de origem mais alta. Esse método não garante convergência. Verifique se a topologia está consistente depois que um conflito é detectado. Para obter mais informações, consulte “Controlando conflitos” em [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 [ @local=] '*local*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @timeout=] *tempo limite*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_configure_peerconflictdetection é usado na replicação transacional ponto a ponto. Para usar a detecção de conflito, todos os nós devem estar em execução [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou versões posteriores; e a detecção devem estar habilitada para todos os nós.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin ou na função de banco de dados fixa db_owner.  
  
## <a name="see-also"></a>Consulte também  
 [Detecção de conflitos na replicação ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
