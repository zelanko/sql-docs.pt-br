---
title: Criar um novo projeto do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- projects [Integration Services], creating
- Integration Services projects, creating
- SQL Server Integration Services projects, creating
- SSIS projects, creating
ms.assetid: 1e23f259-0401-4333-ab4f-89809aae63b1
caps.latest.revision: 51
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fd06f9372092ccbbe221796555c63880d3566f91
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37298726"
---
# <a name="create-a-new-integration-services-project"></a>Criar um novo projeto do Integration Services
  Este procedimento cria um novo projeto e uma nova solução do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
### <a name="to-create-a-new-integration-services-project"></a>Para criar um novo projeto Integration Services  
  
1.  Abra o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**.  
  
3.  Na caixa de diálogo **Novo Projeto**, no painel **Modelos**, selecione o modelo **Projeto do Integration Services**.  
  
     O modelo **Projeto do Integration Services** cria um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém um único pacote vazio.  
  
4.  (Opcional) Edite o nome do projeto e o local.  
  
     O nome da solução é automaticamente atualizado para corresponder ao nome do projeto.  
  
5.  Para criar uma pasta separada para o arquivo de solução, selecione **Criar diretório para solução**. Essa é a opção padrão.  
  
6.  Se o software de controle do código-fonte estiver instalado no computador, selecione **Adicionar ao controle do código-fonte** para associar o projeto ao controle do código-fonte.  
  
7.  Se o software de controle do código-fonte for o [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, a caixa de diálogo **Logon do Visual SourceSafe** será aberta. Em **Logon do Visual SourceSafe**, forneça um nome de usuário, uma senha e o nome do banco de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe. Clique em **Procurar** para localizar o banco de dados.  
  
    > [!NOTE]  
    >  Para exibir e alterar o plug-in de controle do código-fonte selecionado e configurar o ambiente de controle do código-fonte, clique em **Opções** no menu **Ferramentas** e expanda o nó **Controle do Código-fonte**.  
  
8.  Clique em **Okey** para adicionar a solução ao **Gerenciador de soluções**r e adicionar o projeto à solução.  
  
## <a name="see-also"></a>Consulte também  
 [Serviços de integração &#40;SSIS&#41; projetos](integration-services-ssis-projects-and-solutions.md)   
 [Adicionar ou remover um projeto do Integration Services em uma solução](../../2014/integration-services/add-or-remove-an-integration-services-project-in-a-solution.md)  
  
  
