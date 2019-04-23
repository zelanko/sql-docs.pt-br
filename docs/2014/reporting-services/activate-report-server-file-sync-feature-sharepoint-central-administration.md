---
title: Ativar o recurso de sincronização de arquivos de servidor de relatório na Administração Central do SharePoint | Microsoft Docs
ms.prod: reporting-services-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 03/06/2017
ms.openlocfilehash: b56960b23370de3803f475c02aaee3b98ae491e4
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59963942"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-central-administration"></a>Ativar o recurso de sincronização de relatório do Servidor de Relatório na Administração Central do SharePoint

O recurso Sincronização de arquivos do Servidor de Relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] utiliza manipuladores de eventos do SharePoint para sincronizar o catálogo do servidor de relatório com itens em bibliotecas de documentos. Esse recurso é benéfico quando os usuários carregam com frequência itens de relatórios publicados diretamente nas bibliotecas de documentos do SharePoint. Se o recurso de sincronização de arquivos não estiver ativado, conteúdo ainda será sincronizado, mas não com tanta frequência.  
  
O recurso Sincronização de Arquivos pode ser ativado na Administração de Site do SharePoint depois que você instala o Suplemento [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] para produtos do SharePoint.  
  
Esse recurso pode ser ativado e desativado manualmente por site, mas não no nível de conjunto de sites.  
  
## <a name="prerequisites"></a>Prerequisites  
 O Suplemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para o SharePoint deve ser instalado. Se o suplemento não estiver instalado, o recurso de sincronização de arquivos não ficarão visível na lista de recursos do site.  
  
 Para verificar a instalação, exiba a lista de aplicativos instalados no [!INCLUDE[msCoName](../includes/msconame-md.md)] Painel de Controle **do**Windows. Se o Suplemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] estiver instalado, siga as instruções deste tópico para ativar o recurso Sincronização de arquivos do servidor de relatório.  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>Para ativar ou desativar o recurso Sincronização de arquivos do Reporting Services em um site  
  
1.  Na página principal do seu site, clique o **ações do Site** menu e clique em **configurações de Site**.  
  
2.  No **ações do Site**, clique em **gerenciar recursos de Site**.  
  
3.  Localize **Sincronização de arquivos do Servidor de Relatório** na lista.  
  
4.  Clique em **Ativar**.  
  
> [!NOTE]  
>  Para desativar o recurso Sincronização de arquivos do Servidor de Relatório, é possível usar o mesmo procedimento, mas clique em **Desativar**.  
  
## <a name="see-also"></a>Consulte também  
 [Solucionar problemas de partes de relatório &#40;relatórios e SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Instalar ou desinstalar o Reporting Services suplemento para SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Instalar ou desinstalar o Reporting Services suplemento para SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
