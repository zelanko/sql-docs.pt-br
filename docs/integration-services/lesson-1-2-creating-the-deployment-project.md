---
title: 'Etapa 2: Criar o projeto de implantação | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 48f34b1637ce5e388ff5961b984485de8a2e08ab
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723416"
---
# <a name="lesson-1-2---creating-the-deployment-project"></a>Lição 1-2 – criar o projeto de implantação

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


No [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], a unidade que permite a implantação é um projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Antes de implantar os pacotes, você deve criar um novo projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e adicionar todos os pacotes e qualquer arquivo auxiliar que deseja implantar com os pacotes nesse projeto.  
  
### <a name="to-create-the-integration-services-project"></a>Para criar o projeto Integration Services  
  
1.  Clique em **Iniciar**, aponte para **Todos os Programas**, **Microsoft SQL Server**e clique em **SQL Server SQL Server Data Tools**.  
  
2.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto** para criar um novo projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
3.  Na caixa de diálogo **Novo Projeto** , selecione **Projeto do Integration Services** no painel **Modelos** .  
  
4.  Na caixa **Nome** , altere o nome padrão para **Tutorial de Implantação**. Opcionalmente, desmarque a caixa de seleção **Criar diretório para a solução** .  
  
5.  Aceite o local padrão ou clique em **Procurar** para localizar a pasta que você quer usar.  
  
6.  Na caixa de diálogo **Local do Projeto** , clique na pasta e em **Abrir**.  
  
7.  Clique em **OK**.  
  
8.  Por padrão, um pacote vazio, chamado Package.dtsx, é criado e adicionado ao seu projeto. Porém, você não usará este pacote; em vez disso, adicionará os pacotes existentes ao projeto. Como todos os pacotes em um projeto serão incluídos na implantação, você deverá excluir o Package.dtsx. Para excluí-lo, clique nele com o botão direito do mouse e clique em **Excluir**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Etapa 3: Adicionar pacotes e outros arquivos](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
## <a name="see-also"></a>Consulte Também  
[Projetos do Integration Services &#40;SSIS&#41;](~/integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
  

