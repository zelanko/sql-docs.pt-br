---
title: Renomear um banco de dados Multidimensional (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: renaming databases
ms.assetid: 15fdaec7-f3e4-44d9-9b78-1a1d78c484e0
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2e71eba3112c7d7795c7bff342a27e081c5619d9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="rename-a-multidimensional-database-analysis-services"></a>Renomear um bancos de dados multidimensional (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]A maneira na qual você pode alterar o nome de um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados depende de como você se conecta ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados. Para alterar o nome de um banco de dados existente, conecte-se em modo online. Para alterar o nome do banco de dados no qual os objetos de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] serão instanciados, conecte-se em modo de projeto.  
  
### <a name="to-change-the-database-name-in-online-mode"></a>Alterar o nome do banco de dados em modo online  
  
1.  Usando o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], conecte-se diretamente ao banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no banco de dados e clique em **Editar Banco de Dados**.  
  
3.  Na caixa de texto **Nome do Banco de Dados** , altere o nome do banco de dados.  
  
4.  Clique em **Salvar** ou em **Salvar Tudo** na barra de ferramentas, clique em **Salvar Itens Selecionados** ou em **Salvar Tudo** no menu **Arquivo** ou feche o **Designer de Banco de Dados** e, em seguida, clique em **Salvar** quando solicitado.  
  
     O nome de banco de dados é atualizado na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , bem como o objeto de banco de dados no Gerenciador de Soluções.  
  
### <a name="to-change-the-database-name-in-project-mode"></a>Alterar o nome do banco de dados em modo de projeto  
  
1.  Abra o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Páginas de Propriedades** , clique em **Implantação** na seção **Propriedades de Configuração** .  
  
4.  Altere a propriedade **Banco de Dados** com o novo nome do banco de dados.  
  
     Na próxima vez que o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] for implantado, ele será implantado com esse novo nome de banco de dados. Se existir um banco de dados com o mesmo nome, ele será substituído.  
  
### <a name="to-change-the-database-name-using-sql-server-management-studio"></a>Para alterar o nome do banco de dados usando o SQL Server Management Studio  
  
-   Clique com o botão direito do mouse no banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e edite a propriedade Name.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Definir propriedades de banco de dados Multidimensional &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)   
 [Configurar propriedades do projeto do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)   
 [Implantar projetos do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
