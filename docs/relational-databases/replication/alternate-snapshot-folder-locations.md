---
title: "Alternar locais de pasta de instantâneo | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
caps.latest.revision: "36"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3c1d03f6d3d20f821eeb1ab4e8930b06fc0f997e
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="alternate-snapshot-folder-locations"></a>Locais da pasta de instantâneos alternativos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Locais de instantâneos alternativos permitem que você armazene arquivos de instantâneos em outro local ou em local diferente do padrão em que normalmente está localizado no Distribuidor. Locais alternativos podem ficar em outro servidor, em uma unidade de rede ou uma mídia removível (como um CD-ROM ou disco removível).  
  
 Locais de instantâneo alternativos são armazenados como uma propriedade da publicação. Devido ao local de instantâneo alternativo ser uma propriedade da publicação, o Agente de Distribuição e o Agente de Mesclagem podem localizar o instantâneo apropriado como parte do processo de sincronização.  
  
 Para especificar um local de pasta de instantâneo padrão ou compactar arquivos de instantâneo, crie a publicação sem criar o instantâneo inicial imediatamente, defina as propriedades da publicação para o local do instantâneo e execute o Agente de Instantâneo para aquela publicação. Se você alterar o local alternativo após criar o instantâneo inicial, o local de qualquer instantâneo gerado para a publicação não será realocado para o novo local alternativo. Nesse caso, dependendo das configurações da publicação, o Merge Agent ou Distribution Agent talvez não encontrem os arquivos de instantâneo no novo local alternativo.  
  
> [!NOTE]  
>  Não especifique nenhum local alternativo (usando a caixa de diálogo **Propriedades da Publicação** ou [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)) que seja igual ao local da pasta do instantâneo padrão.  
  
> [!CAUTION]  
>  Não use WebSync e locais de pasta de instantâneo alternativos ao mesmo tempo.  
  
 **Para especificar locais de instantâneo alternativos**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Especificar um local de pasta de instantâneo alternativa &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   Programação [!INCLUDE[tsql](../../includes/tsql-md.md)] de replicação: [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de replicação&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Opções de instantâneo](../../relational-databases/replication/snapshot-options.md)  
  
  
