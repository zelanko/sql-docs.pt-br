---
title: Ativar o recurso de sincronização de arquivos de servidor de relatório na Administração Central do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 32d1988d-07e7-41c2-b636-e65ecfae4677
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 83ffe3e16bad4fdc1c60a818dd7f07bd47e00cb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122110"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-central-administration"></a>Ativar o recurso de sincronização de relatório do Servidor de Relatório na Administração Central do SharePoint
  O recurso Sincronização de arquivos do Servidor de Relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] utiliza manipuladores de eventos do SharePoint para sincronizar o catálogo do servidor de relatório com itens em bibliotecas de documentos. Esse recurso é benéfico quando os usuários carregam com frequência itens de relatórios publicados diretamente nas bibliotecas de documentos do SharePoint. Se o recurso de Sincronização de arquivo não estiver ativado, o conteúdo ainda será sincronizado, mas não tão frequentemente.  
  
 O recurso de sincronização de arquivos pode ser ativado na administração de Site do SharePoint depois de instalar o [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] suplemento para produtos do SharePoint.  
  
 Esse recurso pode ser ativado e desativado manualmente por site, mas não no nível de conjunto de sites.  
  
## <a name="prerequisites"></a>Prerequisites  
 O Suplemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para o SharePoint deve ser instalado. Se o suplemento não estiver instalado, o recurso de sincronização de arquivos não estará visível na lista de recursos do site.  
  
 Para verificar a instalação, exiba a lista de aplicativos instalados em [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows **painel de controle**. Se o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] suplemento está instalado, siga as instruções neste tópico para ativar o recurso de sincronização de arquivos de servidor de relatório.  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>Para ativar ou desativar o recurso Sincronização de arquivos do Reporting Services em um site  
  
1.  Na página principal do site, clique no menu **Ações do Site** e clique em **Configurações do Site**.  
  
2.  Em **Ações de Site** , clique em **Gerenciar Recursos de Site**.  
  
3.  Localize **Sincronização de arquivos do Servidor de Relatório** na lista.  
  
4.  Clique em **Ativar**.  
  
> [!NOTE]  
>  Para desativar o recurso Sincronização de arquivos do Servidor de Relatório, é possível usar o mesmo procedimento, mas clique em **Desativar**.  
  
## <a name="see-also"></a>Consulte também  
 [Solucionar problemas de partes de relatório &#40;SSRS e construtor de relatórios&#41;](report-parts-report-builder-and-ssrs.md)   
 [Ativar o servidor de relatório e recursos de integração do Power View no SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Instalar ou desinstalar o Reporting Services suplemento para SharePoint &#40;do SharePoint 2010 e SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Instalar ou desinstalar o Reporting Services suplemento para SharePoint &#40;do SharePoint 2010 e SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  