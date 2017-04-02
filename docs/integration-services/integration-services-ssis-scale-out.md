---
title: "Expans&#227;o do Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Expans&#227;o do Integration Services (SSIS)
A Expansão [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece a execução de alto desempenho do pacote, distribuindo execuções em vários computadores. Você pode de enviar uma solicitação de várias execuções de pacote no SQL Server Management Studio. Esses pacotes serão executados em paralelo, em um modo de expansão.  


## <a name="ssis-scale-out-master-and-scale-out-worker"></a>Mestre de Expansão e Trabalho de Expansão do SSIS
A Expansão [!INCLUDE[ssIS_md](../includes/ssis-md.md)] consiste em um Mestre de Expansão [!INCLUDE[ssIS_md](../includes/ssis-md.md)] e vários Trabalhos de Expansão [!INCLUDE[ssIS_md](../includes/ssis-md.md)]. O Mestre de Expansão é responsável pelo gerenciamento da Expansão e recebe solicitações de execução de pacote dos usuários. Os Trabalhos de Expansão efetuam pull de tarefas de execução do Mestre de Expansão e fazem o trabalho do pacote de execução. Para obter mais informações, consulte [Mestre de Expansão](../integration-services/integration-services-ssis-scale-out-master.md) e [Trabalho de Expansão](../integration-services/integration-services-ssis-scale-out-worker.md).


## <a name="how-to-set-up-scale-out"></a>Como configurar a Expansão
A Expansão [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] pode ser executada em um computador, em que um Mestre de Expansão e um Trabalho de Expansão são configurados lado a lado no computador. A Expansão também pode ser executada em várias máquinas, na qual cada Trabalho de Expansão fica em um computador diferente.
- [Passo a passo: configurar a Expansão do Integration Services](../integration-services/walkthrough-set-up-integration-services-scale-out.md)


## <a name="run-packages-in-scale-out"></a>Executar pacotes em Expansão
A Expansão dá suporte à execução de vários pacotes em paralelo no catálogo do SSISDB. Para obter mais detalhes, consulte [Executar pacotes na Expansão](../integration-services/run-packages-in-integration-services-ssis-scale-out.md).

