---
title: sp_helptracertokens (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_helptracertokens
- sp_helptracertokens_TSQL
helpviewer_keywords:
- sp_helptracertokens
ms.assetid: 61f27234-531d-4b37-8fa3-fe4c32e6f521
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2636da813e83e0efe3efdef7a283ad1ee48293a3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelptracertokens-transact-sql"></a>sp_helptracertokens (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada token de rastreamento que foi inserido em uma publicação para determinar latência. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, ou no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helptracertokens [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação na qual os tokens de rastreamento foram inseridos. *publicação* é **sysname**, sem padrão.  
  
 [  **@publisher=** ] **'***publicador***'**  
 O nome do publicador. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Esse parâmetro só deve ser especificado para não -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 O nome do banco de dados de publicação. *publisher_db* é **sysname**, com um valor padrão de NULL. Esse parâmetro será ignorado se o procedimento armazenado for executado no Publicador.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**Int**|Identifica um registro de token de rastreamento.|  
|**publisher_commit**|**datetime**|A data e hora que o registro do token foi confirmado no Publicador no banco de dados de publicação.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helptracertokens** é usado em replicação transacional.  
  
 **sp_helptracertokens** é usada para obter IDs de token de rastreamento ao executar [sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokens-tran_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa, o **db_owner** função de banco de dados fixa no banco de dados de publicação, ou **db_owner** banco de dados fixo ou  **replmonitor** funções no banco de dados de distribuição podem executar **sp_helptracertokenhistory**.  
  
## <a name="see-also"></a>Consulte também  
 [Medir a latência e validar as conexões para a replicação transacional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
