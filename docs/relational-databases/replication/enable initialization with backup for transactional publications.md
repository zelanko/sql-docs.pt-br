---
title: "Habilitar a inicializa&#231;&#227;o com um backup para publica&#231;&#245;es transacionais (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "inicialização manual de assinaturas [replicação do SQL Server]"
  - "assinaturas [replicação do SQL Server], inicializando"
  - "inicializando assinaturas [replicação do SQL Server], sem instantâneos"
  - "replicação transacional, backup e restauração"
  - "backups [replicação do SQL Server], replicação transacional"
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Habilitar a inicializa&#231;&#227;o com um backup para publica&#231;&#245;es transacionais (SQL Server Management Studio)
  Para inicializar uma assinatura de uma publicação transacional a partir de um backup, habilite a publicação para permitir a inicialização a partir de um backup e então especifique informações de backup ao criar a assinatura.  
  
-   Habilite a publicação na **Opções de assinatura** página o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Especifique informações de backup com o procedimento armazenado [sp_addsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Para obter mais informações sobre os parâmetros exigidos por **sp_addsubscription**, consulte [inicializar uma assinatura transacional de um Backup & #40. Programação Transact-SQL de replicação e 41;](../../relational-databases/replication/initialize a transactional subscription from a backup.md).  
  
### Para habilitar a inicialização com um backup  
  
1.  No **Opções de assinatura** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione um valor de **True** para o **Permitir a inicialização de arquivos de backup** opção.  
  
## Consulte também  
 [Inicializar uma assinatura transacional sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  