---
title: 'Lição 3: adicionando registro em log | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e716b808d5d9ada8aeaf50d92006cc6453c6e47d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67046768"
---
# <a name="lesson-3-adding-logging"></a>Lição 3: Adicionando log
  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui recursos de registro em log que permitem solucionar problemas e monitorar a execução do pacote fornecendo um rastreamento de eventos de tarefa e de contêiner. Os recursos de log são flexíveis, e podem ser habilitados no nível do pacote ou em tarefas individuais e contêineres dentro do pacote. Você pode selecionar quais eventos quer você anotar, e criar múltiplos logs vários em um único pacote.  
  
 O log é fornecido por um provedor de log. Cada provedor de log pode gravar informações de log em diferentes formatos e tipos de destino. 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece os seguintes provedores de log:  
  
-   Arquivo de texto  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Janela Evento de Log  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   Arquivo XML  
  
 Nesta lição, você criará uma cópia do pacote criado na [lição 2: adicionando looping](lesson-2-adding-looping-with-ssis.md). Trabalhando com este novo pacote, você irá adicionar e então configurar o log para monitorar eventos específicos durante a execução de pacote. Se você não tiver completado nenhuma das anteriores lições, poderá também copiar o pacote da Lição 2 terminada, que está inclusa no tutorial.  
  
> [!IMPORTANT]  
>  Este tutorial requer o banco de dados de exemplo **AdventureWorksDW2012** . Para obter mais informações sobre como instalar e implantar o **AdventureWorksDW2012**, [Reporting Services exemplos de produtos no GitHub](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiando o pacote da Lição 2](lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [Etapa 2: Adicionando e configurando registro em log](lesson-3-2-adding-and-configuring-logging.md)  
  
-   [Etapa 3: Testando o pacote de tutorial da Lição 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
 [Etapa 1: Copiando o pacote da Lição 2](lesson-3-1-copying-the-lesson-2-package.md)  
  
  
