---
title: Backup e carregamento de visão geral de hardware para APS PDW
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: Para implantar seu ponta a ponta solução do data warehouse em Analytics Platform System (APS) com SQL Server Parallel Data Warehouse (PDW), você precisa criar um plano de backup do data warehouse e o carregamento de dados.
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 3a2ae046-f8d8-4a5c-b3c1-6ecee005df6c
caps.latest.revision: 9
ms.openlocfilehash: 8979b0d7b14f3e6b3de2834fdc800c5281d057ad
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="backup-and-loading-hardware-overview"></a>Backup e carregamento de visão geral de hardware
Para implantar seu ponta a ponta solução do data warehouse em Analytics Platform System (APS) com SQL Server Parallel Data Warehouse (PDW), você precisa criar um plano de backup do data warehouse e o carregamento de dados. Use este guia para adquirir e configurar servidores de backup e carregar que atenda às suas necessidades de negócios.  
  
## <a name="acquire-and-configure-backup-servers"></a>Adquirir e configurar servidores de backup  
![Processo de backup](media/backup-process.png "processo de Backup")  
  
Para fazer backup de um banco de dados PDW, você precisa de um ou mais servidores de backup. Você pode usar seu próprio hardware existente ou adquirir novo hardware. Para obter mais informações, consulte [adquirir e configurar um servidor de Backup](acquire-and-configure-backup-server.md). Essas instruções incluem um [planilha de planejamento de capacidade do servidor de Backup](backup-capacity-planning-worksheet.md) para ajudá-lo a planejar a solução certa para backup.  
  
## <a name="acquire-and-configure-loading-servers"></a>Adquirir e configurar servidores de carregamento  
![Processo de carregamento](media/loading-process.png "processo de carregamento")  
  
Para carregar dados, você precisa de um ou mais servidores de carregamento. Você pode usar seu próprio ETL existente ou outros servidores, ou você pode adquirir novos servidores. Para obter mais informações, consulte [adquirir e configurar um servidor de carregamento](acquire-and-configure-loading-server.md). Essas instruções incluem um [carregar planilha de planejamento de capacidade do servidor](loading-server-capacity-planning-worksheet.md) para ajudá-lo a planejar a solução certa para carregamento.  
  
## <a name="see-also"></a>Consulte também  
[Visão geral de backup e restauração](backup-and-restore-overview.md)  
[Visão geral de carga](load-overview.md)  
  
