---
title: "Lição 3: Adicionar o registro em log com o SSIS | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0bfc02e0c5930fca3dec339274167cbad5716461
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="lesson-3-add-logging-with-ssis"></a>Lição 3: Adicionar o log com o SSIS
[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui recursos de log que permitem solucionar problemas e monitorar a execução do pacote fornecendo um rastreamento de eventos de tarefa e contêiner. Os recursos de log são flexíveis, e podem ser habilitados no nível do pacote ou em tarefas individuais e contêineres dentro do pacote. Você pode selecionar quais eventos quer você anotar, e criar múltiplos logs vários em um único pacote.  
  
O log é fornecido por um provedor de log. Cada provedor de log pode gravar informações de log em diferentes formatos e tipos de destino. O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece os seguintes provedores de log:  
  
-   Arquivo de texto  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Janela Evento de Log  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   Arquivo XML  
  
Nesta lição, você aprenderá a criar uma cópia do pacote criado em [Lição 2: Adicionando loop com o SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md). Trabalhando com este novo pacote, você irá adicionar e então configurar o log para monitorar eventos específicos durante a execução de pacote. Se você não tiver completado nenhuma das anteriores lições, poderá também copiar o pacote da Lição 2 terminada, que está inclusa no tutorial.  
  
> [!IMPORTANT]  
> Este tutorial requer o banco de dados de exemplo **AdventureWorksDW2012** . Para obter mais informações sobre como instalar e implantar o **AdventureWorksDW2012**, [Reporting Services Product Samples on CodePlex](http://go.microsoft.com/fwlink/p/?LinkID=526910)(Amostras de produto do Reporting Services no CodePlex)  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiando o pacote da lição 2](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [Etapa 2: Adicionando e Configurando registro em log](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
-   [Etapa 3: Testando o pacote de Tutorial da lição 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
[Etapa 1: Copiando o pacote da lição 2](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
  
  

