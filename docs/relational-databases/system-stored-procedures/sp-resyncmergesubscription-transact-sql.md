---
title: sp_resyncmergesubscription (Transact-SQL) | Microsoft Docs
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
- sp_resyncmergesubscription_TSQL
- sp_resyncmergesubscription
helpviewer_keywords:
- sp_resyncmergesubscription
ms.assetid: e04d464a-60ab-4b39-a710-c066025708e6
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 35f5311da7b2d878a738695ee62a65c947f98693
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33000773"
---
# <a name="spresyncmergesubscription-transact-sql"></a>sp_resyncmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sincroniza novamente uma assinatura de mesclagem para um estado de validação conhecido especificado por você. Isso permite impor a convergência ou sincronizar o banco de dados de assinatura para um point-in-time específico, como a última vez em que a validação foi bem-sucedida, ou para uma data específica. O instantâneo não é reaplicado ao ressincronizar uma assinatura usando esse método. Esse procedimento armazenado não é usado para assinaturas de replicação de instantâneo ou assinaturas de replicação transacional. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, ou no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_resyncmergesubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
        , [ @publication = ] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @resync_type = ] resync_type ]  
    [ , [ @resync_date_str = ] resync_date_string ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, com um padrão NULL. Um valor de NULL será válido se o procedimento armazenado for executado no Publicador. Se o procedimento armazenado for executado no Assinante, um Publicador deverá ser especificado.  
  
 [ **@publisher_db** =] **'***publisher_db***'**  
 É o nome do banco de dados de publicação. *publisher_db* é **sysname**, com um padrão NULL. Um valor de NULL será válido se o procedimento armazenado for executado no Publicador, no banco de dados de publicação. Se o procedimento armazenado for executado no Assinante, um Publicador deverá ser especificado.  
  
 [ **@publication** =] **'***publicação***'**  
 É o nome da publicação. *publicação*é **sysname**, sem padrão.  
  
 [ **@subscriber** =] **'***assinante***'**  
 É o nome do Assinante. *assinante* é **sysname**, com um padrão NULL. Um valor de NULL será válido se o procedimento armazenado for executado no Assinante. Se o procedimento armazenado for executado no Publicador, um Assinante deverá ser especificado.  
  
 [ **@subscriber_db** =] **'***subscriber_db***'**  
 É o nome do banco de dados de assinatura. *subscription_db* é **sysname**, com um padrão NULL. Um valor de NULL será válido se o procedimento armazenado for executado no Assinante, no banco de dados de assinatura. Se o procedimento armazenado for executado no Publicador, um Assinante deverá ser especificado.  
  
 [ **@resync_type** =] *resync_type*  
 Define quando a ressincronização deve ser iniciada. *resync_type* é **int**, e pode ser um dos valores a seguir.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**0**|A sincronização inicia a partir do instantâneo inicial. Essa é a opção que mais utiliza recursos, uma vez que todas as alterações desde o instantâneo inicial são reaplicadas ao Assinante.|  
|**1**|A sincronização inicia a partir da última validação bem-sucedida. Todas as gerações novas ou incompletas que tiveram origem desde a última validação bem-sucedida são reaplicadas ao Assinante.|  
|**2**|A sincronização inicia na data fornecida *resync_date_str*. Todas as gerações novas ou incompletas que tiveram origem após essa data são reaplicadas ao Assinante.|  
  
 [  **@resync_date_str=**] *resync_date_string*  
 Define a data quando a ressincronização deve ser iniciada. *resync_date_string* é **nvarchar (30)**, com um padrão NULL. Esse parâmetro é usado quando o *resync_type* é um valor de **2**. A data fornecida é convertida em seu equivalente **datetime** valor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_resyncmergesubscription** é usado em replicação de mesclagem.  
  
 Um valor de **0** para o *resync_type* parâmetro, que reaplica todas as alterações desde o instantâneo inicial, pode ser uso intensivo de recursos, mas possivelmente muito menor do que uma reinicialização completa. Por exemplo, se o instantâneo inicial foi entregue há um mês, esse valor causará a reaplicação dos dados do último mês. Se o instantâneo inicial continha 1 gigabyte (GB) de dados, mas a quantidade de alterações do último mês consistiu em 2 megabytes (MB) de dados alterados, seria mais eficiente reaplicar os dados do que reaplicar todo o instantâneo de 1 GB.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_resyncmergesubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
