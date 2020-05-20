---
title: sp_copysnapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copysnapshot
- sp_copysnapshot_TSQL
helpviewer_keywords:
- sp_copysnapshot
ms.assetid: a012a32f-6f26-45bf-8046-b51cd7fec455
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c9d9eca16209dd9cfc5695ae56daf929d067ab6e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831781"
---
# <a name="sp_copysnapshot-transact-sql"></a>sp_copysnapshot (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Copia a pasta de instantâneo da publicação especificada para a pasta listada no ** \@ destination_folder**. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador. Esse procedimento armazenado é útil para copiar um instantâneo em mídia removível, como CD-ROM.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_copysnapshot [ @publication = ] 'publication', [ @destination_folder = ] 'destination_folder' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação cujo conteúdo do instantâneo deve ser copiado. a *publicação* é **sysname**, sem padrão.  
  
`[ @destination_folder = ] 'destination_folder'`É o nome da pasta em que o conteúdo do instantâneo de publicação deve ser copiado. *destination_folder*é **nvarchar (255)**, sem padrão. O *destination_folder* pode ser um local alternativo, como em outro servidor, em uma unidade de rede ou em mídia removível (como CD-ROMs ou discos removíveis).  
  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante. o *assinante* é sysname, com um padrão de NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'`É o nome do banco de dados de assinatura. *subscriber_db* é sysname, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_copysnapshot** é usado em todos os tipos de replicação. Os assinantes que executam [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a versão 7,0 e anteriores não podem usar o local de instantâneo alternativo.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_copysnapshot**.  
  
## <a name="see-also"></a>Consulte Também  
 [Locais de pastas de instantâneos alternativos](../../relational-databases/replication/snapshot-options.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
