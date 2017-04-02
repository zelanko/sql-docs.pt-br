---
title: "Compactar arquivos de instant&#226;neo (SQL Server Management Studio) | Microsoft Docs"
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
  - "instantâneos [replicação do SQL Server], compactados"
  - "replicação de instantâneo [SQL Server], instantâneos compactados"
ms.assetid: 174ade3e-74a1-4e67-a6da-b874be3ff50f
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Compactar arquivos de instant&#226;neo (SQL Server Management Studio)
  Especifique que os arquivos devem ser compactados no **instantâneo** página do **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### Para compactar arquivos de instantâneo  
  
1.  Sobre o **instantâneo** página do **Propriedades de publicação - \< publicação>** caixa de diálogo:  
  
    1.  Selecione **Colocar os arquivos nesta pasta**, depois clique em **Procurar** para ir para o diretório ou para entrar no caminho de diretório em que os arquivos de instantâneo devem estar armazenados.  
  
        > [!NOTE]  
        >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se forem usadas assinaturas pull, você deve especificar um diretório compartilhado como um caminho universal naming convention (UNC), como \\\computername\snapshot. Para obter mais informações, consulte [proteger a pasta de instantâneo](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
    2.  Desmarque **Colocar os arquivos na pasta padrão** , exceto se for necessário que os arquivos de instantâneo sejam gravados em ambos os locais.  
  
        > [!NOTE]  
        >  Se essa caixa de seleção estiver marcada, os arquivos armazenados na pasta padrão não serão compactados. Arquivos compactados só podem ser armazenados no local alternativo especificado na etapa anterior.  
  
2.  Selecione **Compactar arquivos de instantâneo nesta pasta**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## Consulte também  
 [Configurar propriedades de instantâneo e 40; Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Instantâneos compactados](../../../relational-databases/replication/compressed-snapshots.md)   
 [Inicializar uma assinatura com um instantâneo](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  