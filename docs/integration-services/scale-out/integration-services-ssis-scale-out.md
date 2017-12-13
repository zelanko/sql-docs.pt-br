---
title: SSIS (SQL Server Integration Services) Scale Out | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0277d312ce4dab14e7ba64529e3eb2251a0d2d02
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-ssis-scale-out"></a>Expansão do Integration Services (SSIS)
A Expansão [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece a execução de alto desempenho do pacote, distribuindo execuções em vários computadores. Você pode enviar uma solicitação de várias execuções de pacote no SQL Server Management Studio. Esses pacotes serão executados em paralelo, em um modo de expansão.  

O [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out consiste em um Mestre do [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out e vários Trabalhos do [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out. O Mestre de Expansão é responsável pelo gerenciamento da Expansão e recebe solicitações de execução de pacote dos usuários. Os Trabalhos de Expansão efetuam pull de tarefas de execução do Mestre de Expansão e fazem o trabalho do pacote de execução. Para obter mais informações, consulte [Mestre de Expansão](integration-services-ssis-scale-out-master.md) e [Trabalho de Expansão](integration-services-ssis-scale-out-worker.md).

O [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out pode ser configurado em um computador, em que um Mestre do Scale Out e um Trabalho do Scale Out são configurados lado a lado no computador. A Expansão também pode ser executada em várias máquinas, na qual cada Trabalho de Expansão fica em um computador diferente.
- [Passo a passo: configurar a Expansão do Integration Services](walkthrough-set-up-integration-services-scale-out.md)

A Expansão dá suporte à execução de vários pacotes em paralelo no catálogo do SSISDB. Para obter mais detalhes, consulte [Executar pacotes na Expansão](run-packages-in-integration-services-ssis-scale-out.md).
