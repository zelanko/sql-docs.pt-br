---
title: Habilitar a inicialização com um Backup para publicações transacionais (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f7aa6ce1627250d217cce8778c099a50e668cbd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056726"
---
# <a name="enable-initialization-with-a-backup-for-transactional-publications-sql-server-management-studio"></a>Habilitar a inicialização com um backup para publicações transacionais (SQL Server Management Studio)
  Para inicializar uma assinatura de uma publicação transacional a partir de um backup, habilite a publicação para permitir a inicialização a partir de um backup e então especifique informações de backup ao criar a assinatura.  
  
-   Habilite a publicação na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
-   Especifique informações de backup com o procedimento armazenado [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Para mais informações sobre os parâmetros exigidos por **sp_addsubscription**, consulte [Inicializar uma assinatura transacional de um Backup &#40;programação de Transact-SQL de replicação&#41;](initialize-a-transactional-subscription-from-a-backup.md).  
  
### <a name="to-enable-initialization-with-a-backup"></a>Para habilitar a inicialização com um backup  
  
1.  Na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**, selecione um valor **Verdadeiro** para a opção **Permitir inicialização dos arquivos de backup**.  
  
## <a name="see-also"></a>Consulte também  
 [Inicializar uma assinatura transacional sem um instantâneo](initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
