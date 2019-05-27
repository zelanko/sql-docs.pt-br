---
title: Excluir uma fonte de dados no Gerenciador de soluções (SSAS Multidimensional) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.deleteobjects.f1
helpviewer_keywords:
- data sources [Analysis Services], deleting
- deleting data sources
- removing data sources
ms.assetid: b45441ef-f909-4736-98b9-cc80d0acac99
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1e3b6dc676c11444c8dd45d1874f77942316a462
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075497"
---
# <a name="delete-a-data-source-in-solution-explorer-ssas-multidimensional"></a>excluir uma exibição da fonte de dados no gerenciador de soluções (SSAS multidimensional)
  Você pode excluir um objeto de fonte de dados para removê-lo permanentemente de um projeto de modelo multidimensional do Analysis Services.  
  
 No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], as fontes de dados são a base para a criação de exibições de dados e as exibições da fonte de dados, por sua vez, são utilizadas para definir dimensões, cubos e estruturas de mineração em um projeto ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Portanto, a exclusão de uma fonte de dados pode invalidar outros objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você sempre deve analisar a lista de objetos dependentes que é fornecida antes de excluir o objeto.  
  
> [!IMPORTANT]  
>  As fontes de dados das quais outros objetos dependem não podem ser excluídas de um banco de dados aberto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo online. É preciso excluir todos os objetos do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que dependem dessa fonte de dados antes de excluí-la. Para obter mais informações, consulte [Conectar em Modo Online a um Banco de Dados do Analysis Services](connect-in-online-mode-to-an-analysis-services-database.md).  
  
### <a name="to-delete-a-data-source"></a>Para excluir uma fonte de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto ou conecte-se ao banco de dados do qual você deseja excluir uma fonte de dados.  
  
2.  No **Gerenciador de Soluções**, expanda a pasta **Fontes de Dados** .  
  
3.  Clique com o botão direito do mouse na fonte de dados e, em seguida, clique em **Excluir**. A caixa de diálogo **Excluir Objetos**  aparecerá, mostrando os objetos que serão invalidados se você excluir a fonte de dados. Examine esta lista com cuidado antes de clicar em **OK** para excluir a fonte de dados.  
  
4.  Salve o projeto.  
  
     Depois de excluir uma fonte de dados de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , salve o projeto modificado ou você verá um erro na próxima vez que abrir o projeto, pois faltará o arquivo XML subjacente da fonte de dados excluída quando o projeto tentar carregá-la.  
  
## <a name="see-also"></a>Consulte também  
 [Fontes de dados em modelos multidimensionais](data-sources-in-multidimensional-models.md)   
 [Fontes de dados com suporte no &#40;Multidimensional do SSAS&#41;](supported-data-sources-ssas-multidimensional.md)  
  
  
