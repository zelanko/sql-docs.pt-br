---
title: 'Lição 3: Adicionar um loop com o SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 82c9e9d43195c4980dfcdcb4daf1c0da4ba6b7a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088546"
---
# <a name="lesson-3-add-logging-with-ssis"></a>Lição 3: Adicionar o log com o SSIS

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui recursos de log que permitem solucionar problemas e monitorar a execução do pacote fornecendo um rastreamento de eventos de tarefa e contêiner. Os recursos de registro em log são flexíveis. Você pode habilitar o log no nível do pacote ou em tarefas ou contêineres individuais dentro do pacote. Você seleciona quais eventos deseja anotar e cria vários logs com relação a um único pacote.  
  
Os provedores de log de criam os logs. Cada provedor de log pode gravar informações de log em diferentes formatos e tipos de destino. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece os seguintes provedores de log:  
  
-   Arquivo de texto  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Janela Evento de Log  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   Arquivo XML  
  
Nesta lição, você criar uma cópia do pacote que criou em [Lição 2: Adicionar looping com o SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md). Trabalhando com este novo pacote, você vai adicionar e então configurar o log para monitorar eventos específicos durante a execução de pacote. Se você não tiver completado nenhuma das anteriores lições, poderá também copiar o pacote da Lição 2 terminada, que está inclusa no tutorial.  

> [!NOTE]
> Se você ainda não fez isso, confira a [Lição 1 Pré-requisitos](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).

## <a name="lesson-tasks"></a>Tarefas da lição  
Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiar o pacote da Lição 2](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [Etapa 2: Adicionar e configurar o registro em log](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
-   [Etapa 3: Testar o pacote da Lição 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
[Etapa 1: Copiar o pacote da Lição 2](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
