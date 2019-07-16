---
title: Backup e carregamento de hardware – Parallel Data Warehouse
description: Para implantar seus dados de ponta a ponta no Analytics Platform System (APS) da solução de armazenamento com o Parallel Data Warehouse (PDW), você precisa criar um plano de backup do data warehouse e o carregamento de dados. Use estas diretrizes para adquirir e configurar servidores de backup e de carregamento que atenda às suas necessidades de negócios.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 90f142a8bb86f99ed5cf5d9ff926bdf849060324
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961413"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>Backup e carregamento de visão geral de hardware – Parallel Data Warehouse
Para implantar seus dados de ponta a ponta no Analytics Platform System (APS) da solução de armazenamento com o Parallel Data Warehouse (PDW), você precisa criar um plano de backup do data warehouse e o carregamento de dados. Use estas diretrizes para adquirir e configurar servidores de backup e de carregamento que atenda às suas necessidades de negócios.  
  
## <a name="acquire-and-configure-backup-servers"></a>Adquirir e configurar servidores de backup  
![Processo de backup](media/backup-process.png "processo de Backup")  
  
Para fazer backup de um banco de dados do PDW, você precisa de um ou mais servidores de backup. Você pode usar seu próprio hardware existente ou adquirir novo hardware. Para obter mais informações, consulte [adquirir e configurar um servidor de Backup](acquire-and-configure-backup-server.md). Essas instruções incluem um [planilha de planejamento de capacidade do servidor de Backup](backup-capacity-planning-worksheet.md) para ajudá-lo a planejar a solução certa para o backup.  
  
## <a name="acquire-and-configure-loading-servers"></a>Adquirir e configurar servidores de carregamento  
![Processo de carregamento](media/loading-process.png "processo de carregamento")  
  
Para carregar dados, você precisa de um ou mais servidores de carregamento. Você pode usar seu próprio ETL existente ou outros servidores, ou você pode comprar novos servidores. Para obter mais informações, consulte [adquirir e configurar um servidor de carregamento](acquire-and-configure-loading-server.md). Essas instruções incluem um [carregamento de planilha de planejamento de capacidade do servidor](loading-server-capacity-planning-worksheet.md) para ajudá-lo a planejar a solução certa para o carregamento.  
  
## <a name="see-also"></a>Consulte também  
[Visão geral de backup e restauração](backup-and-restore-overview.md)  
[Visão geral de carga](load-overview.md)  
  
