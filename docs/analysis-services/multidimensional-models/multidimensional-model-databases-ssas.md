---
title: Bancos de dados de modelo multidimensional (SSAS) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ec839c9638b3baf79cba0148cc932ead7820f7b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="multidimensional-model-databases-ssas"></a>Bancos de dados de modelo multidimensional (SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é uma coleção de fontes de dados, exibições da fontes de dados, cubos, dimensões e funções. Opcionalmente, um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode incluir estruturas para mineração de dados e assemblies personalizados que fornecem um modo de você adicionar funções definidas pelo usuário ao banco de dados.  
  
 Os cubos são os objetos de consulta fundamentais no Analysis Services. Ao se conectar a um banco de dados do Analysis Services, via um aplicativo cliente, você se conecta a um cubo dentro desse banco de dados. Um banco de dados poderá conter vários cubos se você estiver reutilizando dimensões, assemblies, funções ou estruturas de mineração em vários contextos.  
  
 Você pode criar e modificar um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] programaticamente ou usando um destes métodos interativos:  
  
-   Implantar um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para uma instância designada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Esse processo cria um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , se ainda não existir na instância um banco de dados com esse nome, e instancia os objetos designados do banco de dados recém-criado. Ao trabalhar dessa forma com um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], as alterações feitas nos objetos do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] entrarão em vigor somente quando o projeto for implantado em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
-   Crie um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vazio em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], e se conectar diretamente a esse banco de dados usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e criar objetos nele (em vez de fazê-lo em um projeto). Ao trabalhar dessa forma com um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , as alterações feitas nos objetos entrarão em vigor no banco de dados ao qual você está se conectando quando o objeto alterado for salvo.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] utiliza a integração com o software de controle do código-fonte para que vários desenvolvedores possam trabalhar ao mesmo tempo com objetos diferentes em um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O desenvolvedor também pode interagir diretamente com um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , em vez de fazê-lo através de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , mas corre o risco de os objetos do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ficarem fora de sincronia com o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que foi usado nessa implantação. Depois da implantação, use o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para administrar o banco de dados do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Também é possível fazer determinadas alterações no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], como em partições e funções, que também podem fazer com os objetos do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fiquem fora de sincronia com o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que foi usado nessa implantação.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 [Anexar e desanexar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
 [Backup e restauração de bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
 [Documentar e gerar scripts de um banco de dados do Analysis Services](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
 [Modificar ou excluir um banco de dados do Analysis Services](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)  
  
 [Mover um banco de dados do Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)  
  
 [Renomear um bancos de dados multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/rename-a-multidimensional-database-analysis-services.md)  
  
 [Nível de compatibilidade de um banco de dados multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)  
  
 [Definir as propriedades de banco de dados multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)  
  
 [Sincronizar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)  
  
 [Alternar um banco de dados do Analysis Services entre os modos ReadOnly e ReadWrite](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
## <a name="see-also"></a>Consulte também  
 [Conectar em Modo Online a um Banco de Dados do Analysis Services](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)   
 [Criar um projeto do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)   
 [Consultando dados multidimensionais com MDX](../../analysis-services/multidimensional-models/mdx/querying-multidimensional-data-with-mdx.md)  
  
  
