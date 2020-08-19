---
description: 'Lição 1-4: Adicionar uma tarefa de Fluxo de Dados ao pacote'
title: 'Etapa 4: Adicionar uma tarefa de Fluxo de Dados ao pacote | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4d920b5f78d2d3e6dd3e557cbac4e50ad7952884
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449644"
---
# <a name="lesson-1-4-add-a-data-flow-task-to-the-package"></a>Lição 1-4: Adicionar uma tarefa de Fluxo de Dados ao pacote

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Depois que você criar os gerenciadores de conexões para os dados de origem e de destino, adicione a tarefa Fluxo de Dados ao seu pacote. Essa tarefa define o mecanismo de Fluxo de Dados que move dados entre as origens e os destinos, além de fornecer funcionalidade para transformar, limpar e modificar os dados à medida que são movidos. A tarefa Fluxo de Dados é onde a maioria do trabalho de um processo de extração, transformação e carregamento (ETL) acontece.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa o fluxo de dados do fluxo de controle.  
  
## <a name="add-a-data-flow-task"></a>Adicionar uma tarefa de Fluxo de Dados  
  
1.  Selecione a guia **Fluxo de Controle**.  
  
2.  No painel da **Caixa de Ferramentas do SSIS**, expanda **Favoritos** e arraste uma **Tarefa de Fluxo de Dados** para a superfície de design da guia **Fluxo de Controle**.  
  
    > [!NOTE]  
    > Se a Caixa de Ferramentas do SSIS não estiver disponível, selecione o menu **SSIS** e selecione a **Caixa de Ferramentas do SSIS** para exibi-la.  

3.  Na superfície de design **Fluxo de Controle**, clique com o botão direito do mouse na nova **Tarefa de Fluxo de Dados**, selecione **Renomear** e altere o nome para **Extrair Dados de Moeda de Exemplo**.  
  
    Forneça nomes exclusivos a todos os componentes que você adicionar a uma superfície de design. Para facilitar o uso e a sustentabilidade, os nomes devem descrever a função de cada componente. Seguir estas diretrizes de nomeação permite que seus pacotes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sejam documentados automaticamente. Outra forma para documentar seus pacotes é usar anotações. Confira mais informações sobre como usar anotações em [Usar anotações em pacotes](../integration-services/use-annotations-in-packages.md).  
  
4.  Clique com o botão direito do mouse na tarefa Fluxo de Dados, selecione **Propriedades** e, na janela Propriedades, verifique se a propriedade **LocaleID** está definida como **Inglês (Estados Unidos)**.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 5: Adicionar e configurar a fonte de arquivo simples](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>Confira também  
[Tarefa de Fluxo de Dados](../integration-services/control-flow/data-flow-task.md)  
  
  
  
