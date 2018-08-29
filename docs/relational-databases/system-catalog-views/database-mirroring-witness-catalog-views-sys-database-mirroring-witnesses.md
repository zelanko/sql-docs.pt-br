---
title: sys. database_mirroring_witnesses (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_witnesses
- sys.database_mirroring_witnesses_TSQL
- database_mirroring_witnesses
- database_mirroring_witnesses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_witnesses catalog view
- witness [SQL Server], sys.database_mirroring_witnesses catalog view
ms.assetid: 0dd5b794-733b-4a3c-b5a4-62f9f1f0f22d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 52a56f07422da3dc0bf78a4560f9f6573000050f
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031324"
---
# <a name="database-mirroring-witness-catalog-views---sysdatabasemirroringwitnesses"></a>Exibições do catálogo de testemunha de espelhamento - do banco de dados sys. database_mirroring_witnesses
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada função testemunha desempenhada por um servidor em uma parceria de espelhamento de banco de dados. 
  
  Em uma sessão de espelhamento de banco de dados, o failover automático requer um servidor testemunha. De modo ideal, a testemunha reside em um computador separado dos servidores principal e espelho. A testemunha não serve o banco de dados. Em vez disso, ela monitora o status dos servidores principal e espelho. Se o servidor principal falhar, a testemunha poderá iniciar o failover automático para o servidor espelho. 
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|Nome das duas cópias do banco de dados na sessão de espelhamento de banco de dados:|  
|**principal_server_name**|**sysname**|Nome de servidor parceiro cuja cópia do banco de dados é, no momento, o banco de dados principal.|  
|**mirror_server_name**|**sysname**|Nome do servidor parceiro cuja cópia do banco de dados é, no momento, o banco de dados espelho.|  
|**safety_level**|**tinyint**|Configuração de segurança de transação para atualizações no banco de dados espelho:<br /><br /> 0 = Estado desconhecido<br /><br /> 1 = Desativado (assíncrono)<br /><br /> 2 = Completo (síncrono)<br /><br /> Usar uma testemunha para um failover automático requer segurança de transação completa, que é o padrão.|  
|**safety_level_desc**|**nvarchar(60)**|Descrição de garantia de segurança de atualizações no banco de dados espelho:<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL|  
|**safety_sequence_number**|**int**|Número de sequência para alterações de atualização **safety_level**.|  
|**role_sequence_number**|**int**|Atualize o número de sequência para mudanças para funções de principal/espelho desempenhadas pelos parceiros de espelhamento.|  
|**mirroring_guid**|**uniqueidentifier**|Identificador da parceria de espelhamento.|  
|**family_guid**|**uniqueidentifier**|Identificador da família de backup para o banco de dados. Usado para detectar estados de restauração correspondentes.|  
|**is_suspended**|**bit**|O espelhamento de banco de dados está suspenso.|  
|**is_suspended_sequence_number**|**int**|Número de sequência para configuração **is_suspended**.|  
|**partner_sync_state**|**tinyint**|Estado de sincronização da sessão de espelhamento:<br /><br /> 5 = os parceiros estão sincronizados. Failover é potencialmente possível. Para obter informações sobre os requisitos para failover, consulte [troca de função durante a um banco de dados de espelhamento de sessão &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md).<br /><br /> 6 = os parceiros não estão sincronizados. Failover impossível no momento.|  
|**partner_sync_state_desc**|**nvarchar(60)**|Descrição do estado de sincronização da sessão de espelhamento:<br /><br /> SYNCHRONIZED<br /><br /> UNSYNCHRONIZED|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Testemunha de espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-witness.md)   
 [sys.database_mirroring &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
