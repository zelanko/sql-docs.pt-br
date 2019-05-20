---
title: Publicando relatórios em um servidor de relatório | Microsoft Docs
ms.date: 06/01/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- production environments [Reporting Services]
- report projects [Reporting Services]
- Debug configuration [Reporting Services]
- report publishing [Reporting Services]
- publishing reports [Reporting Services]
- report properties [Reporting Services]
- Report Designer [Reporting Services], deploying reports
- Production configuration [Reporting Services]
- publishing reports [Reporting Services], production environments
- DebugLocal configuration [Reporting Services]
- deploying [Reporting Services], reports
- Report Designer [Reporting Services], publishing reports
ms.assetid: bd7aa5e0-61ce-43fd-8f74-5d1aeed078bb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bc4d75a6af4441d2030a71306801449ee74a6a02
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65579975"
---
# <a name="publishing-reports-to-a-report-server"></a>Publicando relatórios em um servidor de relatórios
  Depois de criar e testar um relatório ou conjunto de relatórios, você pode usar os recursos implantação do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para publicar os relatórios em um servidor de relatório. Você pode publicar relatórios individuais ou um projeto do Servidor de Relatório que pode incluir vários relatórios e fontes de dados. A publicação de um projeto do Servidor de Relatório é a forma mais fácil de publicar vários relatórios. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa o termo *implantar*, em vez termo *publicar*. Os dois termos significam o mesmo.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] fornece configurações de projeto para gerenciar a publicação de relatórios. A configuração especifica o local do servidor de relatório, a versão do SQL Server Reporting Services instalada no servidor de relatório, se as fontes de dados publicadas no servidor de relatório são substituídas e assim sucessivamente. Por exemplo, a configuração "Debug" pode ser publicada em um servidor diferente da configuração de "release". Além de usar as configurações que o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] fornece, você pode criar configurações adicionais.  
 
## <a name="requirements-to-publish"></a>Requisitos para publicar
A permissão é determinada por segurança baseada em função que é definida por seu administrador de servidor de relatório. As operações de publicação geralmente são concedidas pela **função Publicador**.  
  
## <a name="project-configurations"></a>Configurações de projeto  
 Seu ambiente de relatório pode ter vários servidores de relatórios e versões diferentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalados. Você pode criar várias configurações e, em seguida, usar uma diferente dependendo do cenário de implantação. As configurações de projeto incluem propriedades para compilar relatórios, como a pasta na qual armazenar temporariamente os relatórios criados, e como tratar problemas de compilação. As configurações também têm propriedades que você usa para especificar o local e a versão do servidor de relatório, as pastas no servidor de relatório.  
  
 Por padrão, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] fornece três configurações de projeto: **DebugLocal**, **Debug**e **Release**. A configuração padrão é DebugLocal. Você geralmente usa a configuração DebugLocal para exibir relatórios em uma janela de visualização local, a configuração Debug para publicar relatórios em um servidor de teste e a configuração Release para publicar relatórios em um servidor de produção. A lista suspensa Configurações da Solução na barra de ferramentas padrão mostra uma configuração ativa. Para usar uma configuração diferente, selecione da lista.  
  
 ![ssrs_project_properties](../../reporting-services/reports/media/ssrs-project-properties.png) 
  
 Para obter mais informações, veja o seguinte
 + [Caixa de diálogo Páginas de Propriedades do Projeto](../../reporting-services/tools/project-property-pages-dialog-box.md)
 + [Deployment and Version Support in SQL Server Data Tools](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)
 + [Definir propriedades de implantação para projetos do Reporting Services no SSDT](../../reporting-services/tools/set-deployment-properties-reporting-services.md)
  
## <a name="to-publish-all-reports-in-a-project"></a>Para publicar todos os relatórios em um projeto  
  
No menu **Compilar**, clique em **Implantar \<report project name>**. Como alternativa, no Gerenciador de Soluções, clique com o botão direito do mouse no projeto de relatório e clique em **Implantar**. Você pode visualizar o status do processo de publicação na janela Saída.  
  
Quando você implantar um projeto do Servidor de Relatório, também são implantadas as fontes de dados compartilhadas no projeto de relatório. Todos os relatórios são implantados usando a mesma configuração de projeto: no mesmo servidor de relatório, na mesma pasta no servidor, e assim por diante. Para publicar relatórios em servidores diferentes, publique-os um por um ou somente inclua os relatórios desejados no projeto do Servidor de Relatório. Uma solução pode incluir vários projetos do Servidor de Relatório. Usar vários projetos pode facilitar o gerenciamento da implantação de relatórios, porque você pode usar uma configuração diferente para implantar projetos diferentes. 
  
## <a name="to-publish-a-single-report"></a>Para publicar um relatório simples  
  
No Gerenciador de Soluções, clique com o botão direito do mouse no relatório e clique em **Implantar**. Você pode visualizar o status do processo de publicação na janela Saída.  
  
 Quando você publica um relatório, também precisa implantar as fontes de dados compartilhadas que o relatório usa.   
 Se não quiser publicar todos os relatórios em um projeto, poderá decidir para publicar somente um único. Para fazer isso, selecione uma configuração que implante o relatório (por exemplo, a configuração Release), clique com o botão direito do mouse no relatório e clique em **Implantar**.  
  
 Se um relatório usar uma fonte de dados compartilhada, você precisará também implantar a fonte de dados compartilhada ou o relatório implantado não será executado. Clique com o botão direito do mouse na fonte de dados compartilhada e depois clique em **Implantar**.  
  
 A URL do servidor de destino do servidor de relatório deve ser especificada e você pode alterar as pastas padrão para as quais os relatórios e as fontes de dados compartilhadas devem ser implantados.  

  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Páginas de Propriedades do Projeto](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [Gerenciamento do conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Atualizar relatórios](../../reporting-services/install-windows/upgrade-reports.md)  
  
  
