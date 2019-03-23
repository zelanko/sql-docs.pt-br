---
title: 'Lição 3: Adicionar registro em log | Microsoft Docs'
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
ms.openlocfilehash: 1a3a32b35503ff6dae2e103f46e45a28359b948d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390954"
---
# <a name="lesson-3-adding-logging"></a>Lição 3: Adicionar registro em log
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui recursos de log que permitem solucionar problemas e monitorar a execução do pacote fornecendo um rastreamento de eventos de tarefa e contêiner. Os recursos de log são flexíveis, e podem ser habilitados no nível do pacote ou em tarefas individuais e contêineres dentro do pacote. Você pode selecionar quais eventos quer você anotar, e criar múltiplos logs vários em um único pacote.  
  
 O log é fornecido por um provedor de log. Cada provedor de log pode gravar informações de log em diferentes formatos e tipos de destino. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece os seguintes provedores de log:  
  
-   Arquivo de texto  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Janela Evento de Log  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   Arquivo XML  
  
 Nesta lição, você criará uma cópia do pacote que você criou na [lição 2: Adicionando um loop](lesson-2-adding-looping-with-ssis.md). Trabalhando com este novo pacote, você irá adicionar e então configurar o log para monitorar eventos específicos durante a execução de pacote. Se você não tiver completado nenhuma das anteriores lições, poderá também copiar o pacote da Lição 2 terminada, que está inclusa no tutorial.  
  
> [!IMPORTANT]  
>  Este tutorial requer o banco de dados de exemplo **AdventureWorksDW2012** . Para obter mais informações sobre como instalar e implantar **AdventureWorksDW2012**, [Reporting Services Product Samples CodePlex](https://go.microsoft.com/fwlink/p/?LinkID=52691).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiando o pacote da lição 2](lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [Etapa 2: Adicionando e Configurando registro em log](lesson-3-2-adding-and-configuring-logging.md)  
  
-   [Etapa 3: Testando o pacote de Tutorial da lição 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
 [Etapa 1: Copiando o pacote da lição 2](lesson-3-1-copying-the-lesson-2-package.md)  
  
  
