---
title: Opções de instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1fa6361199b52eabcd8eb321001f6565a5c3d1cb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52753638"
---
# <a name="snapshot-options"></a>Opções de instantâneo
  Há várias opções disponíveis ao inicializar uma assinatura com um instantâneo:  
  
-   Especifique um local alternativo para a pasta de instantâneo em vez do ou além do local da pasta de instantâneo padrão. Para obter mais informações, consulte [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md).  
  
-   Compacte instantâneos para armazenamento em mídias removíveis ou para transferência em uma rede lenta. Para obter mais informações, consulte [Compressed Snapshots](compressed-snapshots.md).  
  
-   Execute scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] antes ou depois que o instantâneo seja aplicado. Para mais informações, consulte [Executar scripts antes e depois da aplicação do instantâneo](execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Transfira arquivos de instantâneo usando o Protocolo de Transferência de Arquivo (FTP). Para obter mais informações, consulte [Transferir instantâneos pelo FTP](transfer-snapshots-through-ftp.md).  
  
## <a name="see-also"></a>Consulte também  
 [Inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md)  
  
  
