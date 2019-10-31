---
title: sp_helpreplfailovermode (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords:
- sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5b9c8322507c78458110f47f579ec333c3e5e7a7
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73142840"
---
# <a name="sp_helpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe o modo de failover atual de uma assinatura. Esse procedimento armazenado é executado no Assinante, em qualquer banco de dados. Para obter mais informações sobre modos de failover, consulte [assinaturas atualizáveis para replicação transacional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` é o nome do Publicador que está participando da atualização deste assinante. o *Publicador* é **sysname**, sem padrão. O Publicador já deve estar configurado para publicação.  
  
`[ @publisher_db = ] 'publisher_db'` é o nome do banco de dados de publicação. *publisher_db* é **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'` é o nome da publicação que está participando da atualização deste assinante. a *publicação*é **sysname**, sem padrão.  
  
`[ @failover_mode_id = ] 'failover_mode_id' OUTPUT` retorna o valor inteiro do modo de failover e é um parâmetro de **saída** . *failover_mode_id* é um **tinyint** com um padrão de **0**. Ele retorna **0** para atualização imediata e **1** para atualização em fila.  
  
 [ **\@failover_mode =** ] **saída de '***failover_mode***'**  
 Retorna o modo no qual são feitas modificações de dados no Assinante. *failover_mode* é um **nvarchar (10)** com um padrão de NULL. É um parâmetro de **saída** .  
  
|Value|Description|  
|-----------|-----------------|  
|**implantação**|Atualização imediata: as atualizações feitas no Assinante são imediatamente propagadas no Publicador, usando 2PC (protocolo de confirmação de duas fases).|  
|**em fila**|Atualização enfileirada: atualizações feitas no Assinante são armazenadas em uma fila.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpreplfailovermode** é usado na replicação de instantâneo ou na replicação transacional para as quais as assinaturas estão habilitadas para atualização imediata com atualização em fila como failover, em caso de falha.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_helpreplfailovermode**.  
  
## <a name="see-also"></a>Consulte Também  
 [Transact &#40;-SQL sp_setreplfailovermode&#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
