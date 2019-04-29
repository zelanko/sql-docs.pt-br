---
title: Adicionar ou remover um projeto do Integration Services em uma solução | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- Integration Services projects, adding
- SQL Server Integration Services projects, adding
- SSIS projects, adding
- projects [Integration Services], adding
ms.assetid: f01f6475-b63c-41dc-82ac-b62162b3adf7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2581aaffaeeba033e92cff305f0e9904cfb9a970
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62837037"
---
# <a name="add-or-remove-an-integration-services-project-in-a-solution"></a>Adicionar ou remover um projeto do Integration Services em uma solução
  Os procedimentos a seguir descrevem como adicionar ou remover um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em uma solução.  
  
 Você só pode adicionar um projeto a uma solução existente, ou remover um projeto de uma solução, quando a solução estiver visível no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Se tiver selecionado a opção **Sempre mostrar solução** no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] exibirá uma solução mesmo quando essa solução tiver somente um projeto. Caso contrário, o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] só exibirá uma solução quando houver mais de um projeto. Os projetos adicionais podem ser projetos do [!INCLUDE[ssIS](../includes/ssis-md.md)] ou de outros tipos.  
  
## <a name="adding-an-integration-services-project"></a>Adicionando um projeto do Integration Services  
 Ao adicionar um projeto, você pode deixar que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] crie um novo projeto em branco ou pode adicionar um projeto que já tenha sido criado em outra solução. Você só pode adicionar um projeto a uma solução existente quando a solução estiver visível em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
#### <a name="to-add-a-new-integration-services-project-to-a-solution"></a>Para adicionar um novo projeto do Integration Services a uma solução  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra a solução à qual deseja adicionar um novo projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e siga um destes procedimentos:  
  
    -   Clique com o botão direito do mouse na solução, escolha **Adicionar** e clique em **Novo Projeto**.  
  
    -   No menu **Arquivo**, aponte para **Adicionar** e clique em **Novo Projeto**.  
  
2.  Na caixa de diálogo **Adicionar Novo Projeto**, clique em **Projeto do Integration Services** no painel **Modelos**.  
  
3.  Se preferir, edite o nome e o local do projeto.  
  
4.  Clique em **OK**.  
  
#### <a name="to-add-an-existing-integration-services-project-to-a-solution"></a>Para adicionar um projeto existente do Integration Services a uma solução  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra a solução à qual deseja adicionar um projeto existente do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e siga um destes procedimentos:  
  
    -   Clique com o botão direito do mouse na solução, aponte a **Adicionar** e escolha **Projeto Existente**.  
  
    -   No menu **Arquivo**, clique em **Adicionar** e escolha **Projeto Existente**.  
  
2.  Na caixa de diálogo **Adicionar Projeto Existente**, navegue até o local ao qual deseja adicionar o projeto e clique em **Abrir**.  
  
3.  O projeto é adicionado à pasta da solução no **Gerenciador de Soluções**.  
  
## <a name="removing-an-integration-services-project"></a>Removendo um projeto do Integration Services  
 Você só pode remover um projeto de uma solução quando a solução estiver visível em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Assim que a solução estiver visível, você poderá remover tudo, exceto um projeto. Quando restar apenas um projeto, o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] não exibirá mais a pasta da solução e o último projeto não poderá ser removido.  
  
#### <a name="to-remove-an-integration-services-project-from-a-solution"></a>Para remover um projeto do Integration Services de uma solução  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra a solução da qual deseja remover um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e, em seguida, clique em **Descarregar Projeto**.  
  
3.  Clique em **OK** para confirmar a remoção.  
  
## <a name="see-also"></a>Consulte também  
 [Serviços de integração &#40;SSIS&#41; projetos](integration-services-ssis-projects-and-solutions.md)   
 [Criar um novo projeto do Integration Services](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
  
