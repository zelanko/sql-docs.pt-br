---
title: Assistente de implantação do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ssis.deploymentwizard.f1
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
caps.latest.revision: 10
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5b5a86bd0c7baa64403640698ab5b94cdb4f2977
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193786"
---
# <a name="integration-services-deployment-wizard"></a>Assistente de Implantação do Integration Services
  O Assistente de Implantação do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] implanta projetos no catálogo SSISDB em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o modelo de implantação de projeto.  
  
 Para iniciar o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Assistente de implantação de um projeto aberto no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], selecione **Deploy** do **projeto** menu. Para iniciar o assistente [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], expanda o **catálogos do Integration Services** > **SSISDB** nó no Pesquisador de objetos, clique com botão direito do **projetos** pasta e clique **implantar projeto**.  
  
 O assistente prossegue nas quatro etapas a seguir. Clique em **próxima** para mover para a próxima etapa, ou **Previous** para retornar à etapa anterior.  
  
1.  **Selecionar fonte** – selecione o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] projeto que você deseja implantar.  
  
2.  **Selecionar destino** – selecionar o destino do projeto.  
  
3.  **Revisão** – exibe suas seleções.  
  
4.  **Implantar/resultados** – implanta o projeto e exibe os resultados.  
  
## <a name="select-source"></a>Selecionar Fonte  
 Para implantar um arquivo de implantação de projeto que você criou, selecione **arquivo de projeto de implantação** e insira o caminho para o arquivo. ispac ou clique em **procurar** encontrá-lo no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] pasta do projeto. Para implantar um projeto residente no catálogo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , selecione **Catálogo do Integration Services**e insira o nome do servidor e o caminho para o projeto no catálogo.  
  
 Se você iniciar o assistente no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], então por padrão o assistente selecionará o projeto aberto como a origem e ignorará esta etapa. Para retornar a esta etapa e selecionar uma fonte diferente, clique em **Previous** ou clique em **Selecionar fonte** no painel esquerdo.  
  
## <a name="select-destination"></a>Selecionar Destino  
 Para selecionar a pasta de destino para o projeto no catálogo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , insira a instância [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou clique em **Procurar** para selecionar de uma lista de servidores. Digite o caminho do projeto no SSISDB ou clique em **Procurar** para selecioná-lo.  
  
 Se você iniciar o assistente no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], então por padrão o assistente selecionará a instância de servidor conectada e inserirá o caminho para o projeto selecionado. Você pode alterar estes valores para implantar o projeto em um local diferente.  
  
## <a name="review"></a>Revisão  
 O assistente permite que você examine as configurações selecionadas antes da implantação do projeto. Você pode alterar suas seleções clicando em **Anterior**ou clicando em qualquer uma das etapas no painel esquerdo.  
  
## <a name="deployresults"></a>Implantar/Resultados  
 Quando você clica em **Deploy** da **revisão** página, o projeto é implantada e o **resultados** página exibe o sucesso ou fracasso de cada ação. Se a ação falhar, clique em **Com falha** na coluna **Resultado** para exibir uma explicação do erro. Clique em **Salvar relatório...**  para salvar os resultados em um arquivo XML.  
  
 Clique em **Fechar** para sair do assistente.  
  
## <a name="see-also"></a>Consulte também  
 [Implantar projetos no servidor do Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [Implantação de projetos e pacotes](packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
