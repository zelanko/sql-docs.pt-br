---
title: "Especificar o local do instant&#226;neo padr&#227;o (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instantâneos [replicação do SQL Server], locais padrão"
  - "locais de instantâneo padrão"
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Especificar o local do instant&#226;neo padr&#227;o (SQL Server Management Studio)
  Especifique o local de instantâneo padrão na página **Pasta de Instantâneo** do Assistente para Configurar Distribuição. Para obter mais informações sobre como usar esse assistente, consulte [Configurar publicação e distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md). Se você criar uma publicação em um servidor que não esteja configurada como Distributor, especifique um local de instantâneo padrão na página **Pasta de Instantâneo** do Assistente para Novas Publicações. Para obter mais informações sobre como usar esse assistente, consulte [criar uma publicação](../../relational-databases/replication/publish/create-a-publication.md).  
  
 Modificar o local do instantâneo padrão no **editores** página o **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo. Para obter mais informações, consulte [Exibir e modificar o distribuidor e propriedades do publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md). Defina a pasta de instantâneo para cada publicação na **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### Para modificar o local do instantâneo padrão.  
  
1.  No **editores** página do **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo, clique no botão Propriedades (**...**) para o Editor para o qual você deseja alterar o local de instantâneo padrão.  
  
2.  No **Propriedades do publicador - \< publicador>** caixa de diálogo, digite um valor para o **pasta de instantâneo padrão** propriedade.  
  
    > [!NOTE]  
    >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se forem usadas assinaturas pull, você deve especificar um diretório compartilhado como um caminho universal naming convention (UNC), como \\\computername\snapshot. Para obter mais informações, consulte [proteger a pasta de instantâneo](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Consulte também  
 [Locais da pasta de instantâneos alternativos](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  