---
title: "Especificar um local de pasta de instant&#226;neo alternativa (SQL Server Management Studio) | Microsoft Docs"
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
  - "instantâneos [replicação do SQL Server], locais de pasta alternativos"
  - "replicação de instantâneo [SQL Server], locais de pasta alternativos"
  - "pastas de instantâneo alternativas [replicação do SQL Server]"
ms.assetid: 9293f0eb-5531-47ec-b6e2-0392823ce5cc
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Especificar um local de pasta de instant&#226;neo alternativa (SQL Server Management Studio)
  Especificar um local de instantâneo alternativo no **instantâneo** página o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### Para especificar um local de instantâneo alternativo  
  
1.  Sobre o **instantâneo** página do **Propriedades de publicação - \< publicação>** caixa de diálogo:  
  
    1.  Selecione **Colocar os arquivos nesta pasta**, depois clique em **Procurar** para ir para o diretório ou para entrar no caminho de diretório em que os arquivos de instantâneo devem estar armazenados.  
  
        > [!NOTE]  
        >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se forem usadas assinaturas pull, você deve especificar um diretório compartilhado como um caminho universal naming convention (UNC), como \\\computername\snapshot. Para obter mais informações, consulte [proteger a pasta de instantâneo](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
    2.  Desmarque **Colocar os arquivos na pasta padrão** , exceto se for necessário que os arquivos de instantâneo sejam gravados em ambos os locais.  
  
     Para compactar os arquivos de instantâneo, selecione **Compactar arquivos de instantâneo neste local**. A compactação é usada normalmente para conexões de largura da banda baixa e locais de instantâneo alternativos em mídia removível, como um CD-ROM.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## Consulte também  
 [Locais da pasta de instantâneos alternativos](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Configurar propriedades de instantâneo e 40; Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Especifique o local do instantâneo padrão & #40. SQL Server Management Studio e 41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Inicializar uma assinatura com um instantâneo](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  