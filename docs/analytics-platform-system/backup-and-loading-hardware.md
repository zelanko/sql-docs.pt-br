---
title: Backup & carregamento de hardware
description: Para implantar sua solução de data warehouse de ponta a ponta no sistema de plataforma de análise (APS) com Parallel data warehouse (PDW), você precisa criar um plano para fazer backup do data warehouse e carregar dados. Use estas diretrizes para adquirir e configurar servidores de backup e de carregamento que atenderão aos seus requisitos de negócios.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4dd4fba91b1507f711a66a88f40b2fa2ea35e1ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401367"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>Visão geral de backup e carregamento de hardware – data warehouse paralelos
Para implantar sua solução de data warehouse de ponta a ponta no sistema de plataforma de análise (APS) com Parallel data warehouse (PDW), você precisa criar um plano para fazer backup do data warehouse e carregar dados. Use estas diretrizes para adquirir e configurar servidores de backup e de carregamento que atenderão aos seus requisitos de negócios.  
  
## <a name="acquire-and-configure-backup-servers"></a>Adquirir e configurar servidores de backup  
![Processo de backup](media/backup-process.png "Processo de backup")  
  
Para fazer backup de um banco de dados PDW, você precisa de um ou mais servidores de backup. Você pode usar seu próprio hardware existente ou comprar um novo hardware. Para obter mais informações, consulte [adquirir e configurar um servidor de backup](acquire-and-configure-backup-server.md). Essas instruções incluem uma [planilha de planejamento de capacidade do servidor de backup](backup-capacity-planning-worksheet.md) para ajudá-lo a planejar a solução certa para backup.  
  
## <a name="acquire-and-configure-loading-servers"></a>Adquirir e configurar servidores de carregamento  
![Processo de carregamento](media/loading-process.png "Processo de carregamento")  
  
Para carregar dados, você precisa de um ou mais servidores de carregamento. Você pode usar seu próprio ETL ou outros servidores existentes ou pode comprar novos servidores. Para obter mais informações, consulte [adquirir e configurar um servidor de carregamento](acquire-and-configure-loading-server.md). Essas instruções incluem uma [planilha de planejamento de capacidade do servidor de carregamento](loading-server-capacity-planning-worksheet.md) para ajudá-lo a planejar a solução certa para o carregamento.  
  
## <a name="see-also"></a>Consulte Também  
[Visão geral de backup e restauração](backup-and-restore-overview.md)  
[Visão geral da carga](load-overview.md)  
  
