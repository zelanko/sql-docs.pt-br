---
title: Compactar arquivos de instantâneo (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], compressed
- snapshot replication [SQL Server], compressed snapshots
ms.assetid: 174ade3e-74a1-4e67-a6da-b874be3ff50f
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c2f58f04d7f3e8655aaf4ad567d34f9042de292a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="compress-snapshot-files-sql-server-management-studio"></a>Compactar arquivos de instantâneo (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifique que os arquivos devem ser compactados na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-compress-snapshot-files"></a>Para compactar arquivos de instantâneo  
  
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**:  
  
    1.  Selecione **Colocar os arquivos nesta pasta**, depois clique em **Procurar** para ir para o diretório ou para entrar no caminho de diretório em que os arquivos de instantâneo devem estar armazenados.  
  
        > [!NOTE]  
        >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se as assinaturas pull forem usadas, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\computername\snapshot. Para obter mais informações, consulte [Proteger uma pasta de instantâneo](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
    2.  Desmarque **Colocar os arquivos na pasta padrão** , exceto se for necessário que os arquivos de instantâneo sejam gravados em ambos os locais.  
  
        > [!NOTE]  
        >  Se essa caixa de seleção estiver marcada, os arquivos armazenados na pasta padrão não serão compactados. Arquivos compactados só podem ser armazenados no local alternativo especificado na etapa anterior.  
  
2.  Selecione **Compactar arquivos de instantâneo nesta pasta**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de Replicação&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Instantâneos compactados](../../../relational-databases/replication/compressed-snapshots.md)   
 [Inicializar uma assinatura com um instantâneo](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
