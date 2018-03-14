---
title: "Opções de instantâneo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e21ada464e4f839f1566f9b9f9aa82dcaec775e
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="snapshot-options"></a>Opções de instantâneo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Há várias opções disponíveis ao inicializar uma assinatura com um instantâneo:  
  
-   Especifique um local alternativo para a pasta de instantâneo em vez do ou além do local da pasta de instantâneo padrão. Para obter mais informações, consulte [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
-   Compacte instantâneos para armazenamento em mídias removíveis ou para transferência em uma rede lenta. Para obter mais informações, consulte [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md).  
  
-   Execute scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] antes ou depois que o instantâneo seja aplicado. Para mais informações, consulte [Executar scripts antes e depois da aplicação do instantâneo](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Transfira arquivos de instantâneo usando o Protocolo de Transferência de Arquivo (FTP). Para obter mais informações, consulte [Transferir instantâneos pelo FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
