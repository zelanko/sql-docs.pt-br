---
title: 'Etapa 2: criar o projeto de implantação | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9c61b2e6941e94dbb8c399380d5b1e43262158af
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436063"
---
# <a name="step-2-creating-the-deployment-project"></a>Etapa 2: Criar o projeto de implantação
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
 [Etapa 3: Adicionando pacotes e outros arquivos](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
![Ícone de Integration Services (pequeno)](media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Projetos do Integration Services &#40;SSIS&#41;](integration-services-ssis-projects-and-solutions.md)  
  
  
