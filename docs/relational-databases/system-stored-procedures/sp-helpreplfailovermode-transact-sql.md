---
title: sp_helpreplfailovermode (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords:
- sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b350ac28a53dbdb544f3dde0b3493cd40436bca3
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031358"
---
# <a name="sphelpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe o modo de failover atual de uma assinatura. Esse procedimento armazenado é executado no Assinante, em qualquer banco de dados. Para obter mais informações sobre modos de failover, consulte [assinaturas atualizáveis para replicação transacional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publisher***'**  
 É o nome do Publicador que está participando da atualização desse Assinante. *Publisher* está **sysname**, sem padrão. O Publicador já deve estar configurado para publicação.  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 É o nome do banco de dados de publicação. *publisher_db* está **sysname**, sem padrão.  
  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação que está participando da atualização desse Assinante. *publicação*está **sysname**, sem padrão.  
  
 [  **@failover_mode_id=**] **'***failover_mode_id***' saída**  
 Retorna o valor inteiro do modo de failover e é um **saída** parâmetro. *failover_mode_id* é um **tinyint** com um padrão de **0**. Ele retorna **0** para atualização imediata e **1** de atualização enfileirada.  
  
 [**@failover_mode=**] **'***failover_mode***' saída**  
 Retorna o modo no qual são feitas modificações de dados no Assinante. *failover_mode* é um **nvarchar (10)** com um padrão NULL. É um **saída** parâmetro.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Imediata**|Atualização imediata: as atualizações feitas no Assinante são imediatamente propagadas no Publicador, usando 2PC (protocolo de confirmação de duas fases).|  
|**em fila**|Atualização enfileirada: atualizações feitas no Assinante são armazenadas em uma fila.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpreplfailovermode** é usado em replicação de instantâneo ou replicação transacional para quais assinaturas são habilitadas para atualização imediata com atualização enfileirada como failover, em caso de falha.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_helpreplfailovermode**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_setreplfailovermode &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
