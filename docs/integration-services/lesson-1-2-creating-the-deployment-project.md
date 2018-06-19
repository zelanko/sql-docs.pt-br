---
title: 'Etapa 2: criar o projeto de implantação | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d0468fa10f703723c9283ecfe523486b834f447b
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35400268"
---
# <a name="lesson-1-2---creating-the-deployment-project"></a>Lição 1-2 – criar o projeto de implantação
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
  
## <a name="see-also"></a>Consulte Também  
[Projetos do Integration Services &#40;SSIS&#41;](~/integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
  

