---
title: Assistente de implantação do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.deploymentwizard.f1
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 721953c31a44a2ea02f480c9830e6347adfd4eb3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66058005"
---
# <a name="integration-services-deployment-wizard"></a>Assistente de Implantação do Integration Services
  O Assistente de Implantação do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] implanta projetos no catálogo SSISDB em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o modelo de implantação de projeto.  
  
 Para iniciar o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] assistente de implantação em um projeto aberto [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]no, selecione **implantar** no menu **projeto** . Para iniciar o assistente no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], expanda o nó **Integration Services catálogos** > **SSISDB** no Pesquisador de objetos, clique com o botão direito do mouse na pasta **projetos** e clique em **implantar projeto**.  
  
 O assistente prossegue nas quatro etapas a seguir. Clique em **Avançar** para ir para a próxima etapa ou **anterior** para retornar à etapa anterior.  
  
1.  **Selecionar origem** – selecione o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] projeto que você deseja implantar.  
  
2.  **Selecione destino** -selecione o destino do projeto.  
  
3.  **Revisão** – exibe suas seleções.  
  
4.  **Implantar/resultados** – implanta o projeto e exibe os resultados.  
  
## <a name="select-source"></a>Selecionar fonte  
 Para implantar um arquivo de implantação de projeto que você criou, selecione **arquivo de implantação do projeto** e insira o caminho para o arquivo. ispac ou clique em **procurar** para localizá-lo na pasta do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto. Para implantar um projeto residente no catálogo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , selecione **Catálogo do Integration Services**e insira o nome do servidor e o caminho para o projeto no catálogo.  
  
 Se você iniciar o assistente no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], então por padrão o assistente selecionará o projeto aberto como a origem e ignorará esta etapa. Para retornar a esta etapa e selecionar uma fonte diferente, clique em **anterior** ou clique em **selecionar origem** no painel esquerdo.  
  
## <a name="select-destination"></a>Selecionar Destino  
 Para selecionar a pasta de destino para o projeto no catálogo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , insira a instância [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou clique em **Procurar** para selecionar de uma lista de servidores. Digite o caminho do projeto no SSISDB ou clique em **Procurar** para selecioná-lo.  
  
 Se você iniciar o assistente no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], então por padrão o assistente selecionará a instância de servidor conectada e inserirá o caminho para o projeto selecionado. Você pode alterar estes valores para implantar o projeto em um local diferente.  
  
## <a name="review"></a>Análise  
 O assistente permite que você examine as configurações selecionadas antes da implantação do projeto. Você pode alterar suas seleções clicando em **Anterior**ou clicando em qualquer uma das etapas no painel esquerdo.  
  
## <a name="deployresults"></a>Implantar/Resultados  
 Quando você clica em **implantar** na página **revisão** , o projeto é implantado e a página **resultados** exibe o êxito ou a falha de cada ação. Se a ação falhar, clique em **Com falha** na coluna **Resultado** para exibir uma explicação do erro. Clique em **Salvar relatório...** para salvar os resultados em um arquivo XML.  
  
 Clique em **Fechar** para sair do assistente.  
  
## <a name="see-also"></a>Consulte Também  
 [Implantar projetos no Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [Implantação de projetos e pacotes](packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
