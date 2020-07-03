---
title: sp_resyncmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resyncmergesubscription_TSQL
- sp_resyncmergesubscription
helpviewer_keywords:
- sp_resyncmergesubscription
ms.assetid: e04d464a-60ab-4b39-a710-c066025708e6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 48dac5345df6d9e963f3601741aa93a68e2dfa3f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899227"
---
# <a name="sp_resyncmergesubscription-transact-sql"></a>sp_resyncmergesubscription (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Sincroniza novamente uma assinatura de mesclagem para um estado de validação conhecido especificado por você. Isso permite impor a convergência ou sincronizar o banco de dados de assinatura para um point-in-time específico, como a última vez em que a validação foi bem-sucedida, ou para uma data específica. O instantâneo não é reaplicado ao ressincronizar uma assinatura usando esse método. Esse procedimento armazenado não é usado para assinaturas de replicação de instantâneo ou assinaturas de replicação transacional. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, ou no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador* é **sysname**, com um padrão de NULL. Um valor de NULL será válido se o procedimento armazenado for executado no Publicador. Se o procedimento armazenado for executado no Assinante, um Publicador deverá ser especificado.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados de publicação. *publisher_db* é **sysname**, com um padrão de NULL. Um valor de NULL será válido se o procedimento armazenado for executado no Publicador, no banco de dados de publicação. Se o procedimento armazenado for executado no Assinante, um Publicador deverá ser especificado.  
  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação*é **sysname**, sem padrão.  
  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante. o *assinante* é **sysname**, com um padrão de NULL. Um valor de NULL será válido se o procedimento armazenado for executado no Assinante. Se o procedimento armazenado for executado no Publicador, um Assinante deverá ser especificado.  
  
`[ @subscriber_db = ] 'subscriber_db'`É o nome do banco de dados de assinatura. *subscription_db* é **sysname**, com um padrão de NULL. Um valor de NULL será válido se o procedimento armazenado for executado no Assinante, no banco de dados de assinatura. Se o procedimento armazenado for executado no Publicador, um Assinante deverá ser especificado.  
  
`[ @resync_type = ] resync_type`Define quando a ressincronização deve ser iniciada em. *resync_type* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|A sincronização inicia a partir do instantâneo inicial. Essa é a opção que mais utiliza recursos, uma vez que todas as alterações desde o instantâneo inicial são reaplicadas ao Assinante.|  
|**1**|A sincronização inicia a partir da última validação bem-sucedida. Todas as gerações novas ou incompletas que tiveram origem desde a última validação bem-sucedida são reaplicadas ao Assinante.|  
|**2**|A sincronização começa a partir da data fornecida em *resync_date_str*. Todas as gerações novas ou incompletas que tiveram origem após essa data são reaplicadas ao Assinante.|  
  
`[ @resync_date_str = ] resync_date_string`Define a data em que a ressincronização deve ser iniciada em. *resync_date_string* é **nvarchar (30)**, com um padrão de NULL. Esse parâmetro é usado quando o *resync_type* é um valor de **2**. A data fornecida é convertida em seu valor **DateTime** equivalente.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_resyncmergesubscription** é usado na replicação de mesclagem.  
  
 Um valor de **0** para o parâmetro *resync_type* , que Reaplica todas as alterações desde o instantâneo inicial, pode ser com uso intensivo de recursos, mas possivelmente muito menos do que uma reinicialização completa. Por exemplo, se o instantâneo inicial foi entregue há um mês, esse valor causará a reaplicação dos dados do último mês. Se o instantâneo inicial continha 1 gigabyte (GB) de dados, mas a quantidade de alterações do último mês consistiu em 2 megabytes (MB) de dados alterados, seria mais eficiente reaplicar os dados do que reaplicar todo o instantâneo de 1 GB.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_resyncmergesubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
