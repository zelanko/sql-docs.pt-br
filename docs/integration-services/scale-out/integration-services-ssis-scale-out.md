---
title: "SQL Server Integration Services (SSIS) de expansão | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ce7fb96901e8af4da74392fe0a0a85c6e2ec05a4
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out"></a>Expansão do Integration Services (SSIS)
A Expansão [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece a execução de alto desempenho do pacote, distribuindo execuções em vários computadores. Você pode enviar uma solicitação para várias execuções de pacote no SQL Server Management Studio. Esses pacotes serão executados em paralelo, em um modo de expansão.  

[!INCLUDE[ssIS_md](../../includes/ssis-md.md)]Expansão consiste em uma [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] escala Out mestre e um ou mais [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] operadores fora de escala. O Mestre de Expansão é responsável pelo gerenciamento da Expansão e recebe solicitações de execução de pacote dos usuários. Os Trabalhos de Expansão efetuam pull de tarefas de execução do Mestre de Expansão e fazem o trabalho do pacote de execução. Para obter mais informações, consulte [Mestre de Expansão](integration-services-ssis-scale-out-master.md) e [Trabalho de Expansão](integration-services-ssis-scale-out-worker.md).

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]Expansão pode ser configurada em uma máquina, onde um mestre de fora de escala e um trabalho de fora de escala são configurados lado a lado no computador. A Expansão também pode ser executada em várias máquinas, na qual cada Trabalho de Expansão fica em um computador diferente.
- [Passo a passo: configurar a Expansão do Integration Services](walkthrough-set-up-integration-services-scale-out.md)

A Expansão dá suporte à execução de vários pacotes em paralelo no catálogo do SSISDB. Para obter mais detalhes, consulte [Executar pacotes na Expansão](run-packages-in-integration-services-ssis-scale-out.md).

