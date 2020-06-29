---
title: Desenvolvimento de um projeto de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Integration Services], creating
- Integration Services projects, creating
- SQL Server Integration Services projects, creating
- SSIS projects, creating
ms.assetid: 6e90b016-36a5-415e-9440-a20199fffff0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: da648b3b09b25fa2a7b1cf886ad1bf770296f5ef
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85429573"
---
# <a name="development-of-an-integration-services-project"></a>Implantação de um projeto do Integration Services
  Você adiciona pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] a projetos. Para criar e trabalhar com projetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , você deve instalar o ambiente do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] . Para obter mais informações, consulte [Instalar o Integration Services](install-windows/install-integration-services.md).  
  
 Quando você cria um novo projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], a caixa de diálogo **Novo Projeto** inclui um modelo do **Integration Services Project** . Este modelo de projeto cria um novo projeto que contém um único pacote.  
  
## <a name="projects-and-solutions"></a>Soluções e Projetos  
 Projetos são armazenados em soluções. Você pode primeiro criar uma solução e, então, adicionar um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] à solução. Se não existir uma solução, ela será criada automaticamente pelo [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] quando o projeto for criado pela primeira vez. Uma solução pode conter vários projetos de tipos diferentes.  
  
> [!NOTE]  
>  Por padrão, quando você cria um novo projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], a solução não é mostrada no painel **Gerenciador de Soluções** . Para alterar este comportamento padrão, no menu **Ferramentas** , clique em **Opções**. Na caixa de diálogo **Opções** , expanda **Projetos e Soluções**e clique em **Geral**. Na página **Geral** , selecione **Sempre mostrar solução**.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Criar um novo projeto do Integration Services](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
-   [Adicionar um item a um projeto do Integration Services](../../2014/integration-services/add-an-item-to-an-integration-services-project.md)  
  
-   [Adicionar ou remover um projeto do Integration Services em uma solução](../../2014/integration-services/add-or-remove-an-integration-services-project-in-a-solution.md)  
  
  
