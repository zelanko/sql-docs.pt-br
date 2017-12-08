---
title: "Excluir uma fonte de dados no Gerenciador de soluções (SSAS Multidimensional) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.deleteobjects.f1
helpviewer_keywords:
- data sources [Analysis Services], deleting
- deleting data sources
- removing data sources
ms.assetid: b45441ef-f909-4736-98b9-cc80d0acac99
caps.latest.revision: "46"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8e3a98d8d962d3f0bdbe3a818d8496ecdb8a1a94
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="delete-a-data-source-in-solution-explorer-ssas-multidimensional"></a>excluir uma exibição da fonte de dados no gerenciador de soluções (SSAS multidimensional)
  Você pode excluir um objeto de fonte de dados para removê-lo permanentemente de um projeto de modelo multidimensional do Analysis Services.  
  
 No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], as fontes de dados são a base para a criação de exibições de dados e as exibições da fonte de dados, por sua vez, são utilizadas para definir dimensões, cubos e estruturas de mineração em um projeto ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Portanto, a exclusão de uma fonte de dados pode invalidar outros objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você sempre deve analisar a lista de objetos dependentes que é fornecida antes de excluir o objeto.  
  
> [!IMPORTANT]  
>  As fontes de dados das quais outros objetos dependem não podem ser excluídas de um banco de dados aberto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo online. É preciso excluir todos os objetos do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que dependem dessa fonte de dados antes de excluí-la. Para obter mais informações, consulte [Conectar em Modo Online a um Banco de Dados do Analysis Services](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md).  
  
### <a name="to-delete-a-data-source"></a>Para excluir uma fonte de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto ou conecte-se ao banco de dados do qual você deseja excluir uma fonte de dados.  
  
2.  No **Gerenciador de Soluções**, expanda a pasta **Fontes de Dados** .  
  
3.  Clique com o botão direito do mouse na fonte de dados e, em seguida, clique em **Excluir**. A caixa de diálogo **Excluir Objetos**  aparecerá, mostrando os objetos que serão invalidados se você excluir a fonte de dados. Examine esta lista com cuidado antes de clicar em **OK** para excluir a fonte de dados.  
  
4.  Salve o projeto.  
  
     Depois de excluir uma fonte de dados de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , salve o projeto modificado ou você verá um erro na próxima vez que abrir o projeto, pois faltará o arquivo XML subjacente da fonte de dados excluída quando o projeto tentar carregá-la.  
  
## <a name="see-also"></a>Consulte também  
 [Fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Fontes de dados com suporte &#40;SSAS – Multidimensional&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
