---
title: sp_copymergesnapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copymergesnapshot
- sp_copymergesnapshot_TSQL
helpviewer_keywords:
- sp_copymergesnapshot
ms.assetid: eaecd6e0-8486-4e5d-ace7-8ae75768c0a8
author: stevestein
ms.author: sstein
ms.openlocfilehash: d51f29399487ee156210e96fe598c38288755913
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381708"
---
# <a name="sp_copymergesnapshot-transact-sql"></a>sp_copymergesnapshot (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Copia a pasta de instantâneo da publicação especificada para a pasta listada no **\@destination_folder**. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_copymergesnapshot [ @publication = ] 'publication', [ @destination_folder = ] 'destination_folder'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` é o nome da publicação cujo conteúdo do instantâneo deve ser copiado. a *publicação* é **sysname**, sem padrão.  
  
`[ @destination_folder = ] 'destination_folder'` é o nome da pasta onde o conteúdo do instantâneo de publicação deve ser copiado. *destination_folder*é **nvarchar (255)** , sem padrão. O *destination_folder* pode ser um local alternativo, como em outro servidor, em uma unidade de rede ou em mídia removível (como CD-ROMs ou discos removíveis).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_copymergesnapshot** é usado na replicação de mesclagem. Os assinantes que executam [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7,0 e anteriores não podem usar o local de instantâneo alternativo.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_copymergesnapshot**.  
  
## <a name="see-also"></a>Consulte Também  
 [Locais da pasta de instantâneos alternativos](../../relational-databases/replication/snapshot-options.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
