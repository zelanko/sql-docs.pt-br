---
title: "Locais da pasta de instant&#226;neos alternativos | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instantâneos [replicação do SQL Server], locais de pasta alternativos"
  - "replicação de instantâneo [SQL Server], locais de pasta alternativos"
  - "pastas de instantâneo alternativas [replicação do SQL Server]"
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Locais da pasta de instant&#226;neos alternativos
  Locais de instantâneos alternativos permitem que você armazene arquivos de instantâneos em outro local ou em local diferente do padrão onde normalmente está localizado no Distribuidor. Locais alternativos podem ficar em outro servidor, em uma unidade de rede ou uma mídia removível (como um CD-ROM ou disco removível).  
  
 Locais de instantâneo alternativos são armazenados como uma propriedade da publicação. Devido ao local de instantâneo alternativo ser uma propriedade da publicação, o Agente de Distribuição e o Agente de Mesclagem podem localizar o instantâneo apropriado como parte do processo de sincronização.  
  
 Para especificar um local de pasta de instantâneo padrão ou compactar arquivos de instantâneo, crie a publicação sem criar o instantâneo inicial imediatamente, defina as propriedades da publicação para o local do instantâneo e execute o Agente de Instantâneo para aquela publicação. Se você alterar o local alternativo após criar o instantâneo inicial, o local de qualquer instantâneo gerado para a publicação não será realocado para o novo local alternativo. Nesse caso, dependendo das configurações da publicação, o Merge Agent ou Distribution Agent talvez não encontrem os arquivos de instantâneo no novo local alternativo.  
  
> [!NOTE]  
>  Não especificar um local alternativo (usando o **Propriedades de publicação** caixa de diálogo ou [sp_changepublication & #40. Transact-SQL & 41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)) é o mesmo local da pasta de instantâneo padrão.  
  
> [!CAUTION]  
>  Não use WebSync e locais de pasta de instantâneo alternativos ao mesmo tempo.  
  
 **Para especificar locais de instantâneo alternativos**  
  
-   [! INCLUIR [ssManStudioFull] (... / Token/ssManStudioFull_md.md)]: [Specify an Alternate Snapshot Folder Location &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   Replicação [!INCLUDE[tsql](../../includes/tsql-md.md)] programação: [40; & Configurar propriedades de instantâneo Programação Transact-SQL de replicação e 41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## Consulte também  
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Opções de instantâneo](../../relational-databases/replication/snapshot-options.md)  
  
  