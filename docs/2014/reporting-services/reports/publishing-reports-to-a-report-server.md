---
title: Publicando relatórios em um servidor de relatório | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
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
manager: kfile
ms.openlocfilehash: 5c73e75bbdf458b27d0f879a91e72ececc832b88
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66102489"
---
# <a name="publishing-reports-to-a-report-server"></a>Publicando relatórios em um servidor de relatórios
  Depois que você criar e testar um relatório ou conjunto de relatórios, você pode usar os recursos internos de implantação no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para publicar os relatórios em um servidor de relatório. Você pode publicar relatórios individuais ou um projeto do Servidor de Relatório. A publicação de um projeto do Servidor de Relatório é a forma mais fácil de publicar vários relatórios. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa o termo *implante*, em vez termo *publicar*. Os dois termos significam o mesmo.  
  
 Antes de publicar um relatório, você deve ter permissão para fazer isso. A permissão é determinada por segurança baseada em função que é definida por seu administrador de servidor de relatório. As operações de publicação geralmente são concedidas pela função do Publicador.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] fornece configurações de projeto para gerenciar a publicação de relatórios. A configuração especifica o local do servidor de relatório, a versão do SQL Server Reporting Services instalada no servidor de relatório, se as fontes de dados publicadas no servidor de relatório são substituídas e assim sucessivamente. Além de usar as configurações que o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] fornece, você pode criar configurações adicionais.  
  
## <a name="project-configurations"></a>Configurações de projeto  
 Os relatórios são compilados antes de serem publicados para garantir que somente são publicadas definições de relatório válidas para o servidor de relatório. As configurações de projeto incluem propriedades para compilar relatórios, como a pasta na qual armazenar temporariamente os relatórios criados, e como tratar problemas de compilação. As configurações também têm propriedades que você usa para especificar o local e a versão do servidor de relatório, as pastas no servidor de relatório.  
  
 Por padrão, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] fornece três configurações de projeto: DebugLocal, Debug e Release. A configuração padrão é DebugLocal. Você geralmente usa a configuração DebugLocal para exibir relatórios em uma janela de visualização local, a configuração Debug para publicar relatórios em um servidor de teste e a configuração Release para publicar relatórios em um servidor de produção. A lista suspensa Configurações da Solução na barra de ferramentas padrão mostra uma configuração ativa. Para usar uma configuração diferente, selecione da lista.  
  
 Seu ambiente de relatório pode ter vários servidores de relatórios e versões diferentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalados. Você pode criar várias configurações e, em seguida, usar uma diferente dependendo do cenário de implantação. Para obter mais informações, consulte [implantação e suporte de versão no SQL Server Data Tools &#40;SSRS&#41; ](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md) e [definir propriedades de implantação &#40;Reporting Services&#41;](../tools/set-deployment-properties-reporting-services.md).  
  
## <a name="publishing-reports"></a>Publicando relatórios  
 Você pode publicar um único relatório ou um projeto do Servidor de Relatório que contêm vários relatórios. Para obter instruções sobre como publicar relatórios, consulte [publicar relatórios](../publish-reports.md).  
  
### <a name="publishing-a-single-report"></a>Publicando um único relatório  
 Se não quiser publicar todos os relatórios em um projeto, poderá decidir para publicar somente um único. Para fazer isso, selecione uma configuração que implante o relatório (por exemplo, a configuração Release), clique com o botão direito do mouse no relatório e clique em **Implantar**.  
  
 Se um relatório usar uma fonte de dados compartilhada, você precisará também implantar a fonte de dados compartilhada ou o relatório implantado não será executado. Clique com o botão direito do mouse na fonte de dados compartilhada e depois clique em **Implantar**.  
  
 A URL do servidor de destino do servidor de relatório deve ser especificada e você pode alterar as pastas padrão para as quais os relatórios e as fontes de dados compartilhadas devem ser implantados.  
  
### <a name="publishing-multiple-reports"></a>Publicando vários relatórios  
 Quando você publica um projeto de Servidor de Relatório, você publica todos os relatórios nesse projeto. Todos os relatórios são implantados usando a mesma configuração de projeto: no mesmo servidor de relatório, na mesma pasta no servidor, e assim por diante. Para publicar relatórios em servidores diferentes, publique-os um por um ou somente inclua os relatórios desejados no projeto do Servidor de Relatório. Uma solução pode incluir vários projetos do Servidor de Relatório. Usar vários projetos pode facilitar o gerenciamento da implantação de relatórios, porque você pode usar uma configuração diferente para implantar projetos diferentes.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Páginas de Propriedades do Projeto](../tools/project-property-pages-dialog-box.md)   
 [Gerenciamento do conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [Atualizar relatórios](../install-windows/upgrade-reports.md)  
  
  
