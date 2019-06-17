---
title: Publicar relatórios | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], publishing
- publishing reports [Reporting Services]
ms.assetid: ef5a514e-e818-4041-a8b0-15835f9a046b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86ab056f18e69b0b264525377efb0d257ebc2b95
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108025"
---
# <a name="publish-reports"></a>Publicar Relatórios
  No[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], é possível publicar todos os relatórios e fontes de dados compartilhadas em um projeto do Servidor de Relatório implantando um projeto ou publicar um único relatório. Antes de publicar um relatório, você deve especificar a URL do servidor de relatório de destino. Para obter mais informações, consulte [Definir propriedades de implantação &#40;Reporting Services&#41;](tools/set-deployment-properties-reporting-services.md).  
  
 Você pode usar a versão do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para abrir, modificar, visualizar, salvar e publicar relatórios do [!INCLUDE[ssRSversion2005](../includes/ssrsversion2005-md.md)] e do [!INCLUDE[ssRSversion10](../includes/ssrsversion10-md.md)] . Para obter mais informações, veja [Implantação e suporte de versão no SQL Server Data Tools &#40;SSRS&#41;](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
### <a name="to-publish-all-reports-in-a-project"></a>Para publicar todos os relatórios em um projeto  
  
-   No menu **Compilar**, clique em **Implantar \<report project name>** . Como alternativa, no Gerenciador de Soluções, clique com o botão direito do mouse no projeto de relatório e clique em **Implantar**. Você pode visualizar o status do processo de publicação na janela Saída.  
  
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
  
  
