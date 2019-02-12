---
title: Publicar relatórios | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], publishing
- publishing reports [Reporting Services]
ms.assetid: ef5a514e-e818-4041-a8b0-15835f9a046b
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a19db72ae854ae3ffaf4b56587642ddb37e22e0d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032397"
---
# <a name="publish-reports"></a>Publicar Relatórios
  No[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], é possível publicar todos os relatórios e fontes de dados compartilhadas em um projeto do Servidor de Relatório implantando um projeto ou publicar um único relatório. Antes de publicar um relatório, você deve especificar a URL do servidor de relatório de destino. Para obter mais informações, consulte [Definir propriedades de implantação &#40;Reporting Services&#41;](tools/set-deployment-properties-reporting-services.md).  
  
 Você pode usar a versão do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para abrir, modificar, visualizar, salvar e publicar relatórios do [!INCLUDE[ssRSversion2005](../includes/ssrsversion2005-md.md)] e do [!INCLUDE[ssRSversion10](../includes/ssrsversion10-md.md)] . Para obter mais informações, veja [Implantação e suporte de versão no SQL Server Data Tools &#40;SSRS&#41;](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
### <a name="to-publish-all-reports-in-a-project"></a>Para publicar todos os relatórios em um projeto  
  
-   No menu **Compilar**, clique em **Implantar \<report project name>**. Como alternativa, no Gerenciador de Soluções, clique com o botão direito do mouse no projeto de relatório e clique em **Implantar**. Você pode visualizar o status do processo de publicação na janela Saída.  
  
    > [!NOTE]  
    >  Quando você implantar um projeto do Servidor de Relatório, também são implantadas as fontes de dados compartilhadas no projeto de relatório.  
  
### <a name="to-publish-a-single-report"></a>Para publicar um relatório simples  
  
-   No Gerenciador de Soluções, clique com o botão direito do mouse no relatório e clique em **Implantar**. Você pode visualizar o status do processo de publicação na janela Saída.  
  
    > [!NOTE]  
    >  Quando você publica um relatório, também precisa implantar as fontes de dados compartilhadas que o relatório usa.  
  
## <a name="see-also"></a>Consulte também  
 [Publicando fontes de dados e relatórios](reports/publishing-data-sources-and-reports.md)   
 [Visualizar relatórios](reports/previewing-reports.md)   
 [Publicando relatórios em um servidor de relatório](reports/publishing-reports-to-a-report-server.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportando relatórios &#40;relatórios e SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
