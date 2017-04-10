---
title: "Op&#231;&#245;es de instant&#226;neo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicação de instantâneo [SQL Server], opções"
  - "instantâneos [replicação do SQL Server], opções"
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# Op&#231;&#245;es de instant&#226;neo
  Há várias opções disponíveis ao inicializar uma assinatura com um instantâneo:  
  
-   Especifique um local alternativo para a pasta de instantâneo em vez do ou além do local da pasta de instantâneo padrão. Para obter mais informações, consulte [locais de pasta de instantâneo alternativo](../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
-   Compacte instantâneos para armazenamento em mídias removíveis ou para transferência em uma rede lenta. Para obter mais informações, consulte [instantâneos compactados](../../relational-databases/replication/compressed-snapshots.md).  
  
-   Execute scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] antes ou depois que o instantâneo seja aplicado. Para obter mais informações, consulte [Executar Scripts antes e após a aplicação do instantâneo](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Transfira arquivos de instantâneo usando o Protocolo de Transferência de Arquivo (FTP). Para obter mais informações, consulte [Transferir instantâneos pelo FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
## Consulte também  
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  