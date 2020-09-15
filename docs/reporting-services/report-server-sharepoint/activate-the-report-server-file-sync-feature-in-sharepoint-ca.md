---
title: Ativar o recurso de sincronização de arquivo do servidor de relatório no SharePoint | Microsoft Docs
description: O recurso Sincronização de Arquivos do Servidor de Relatório do Reporting Services utiliza manipuladores de eventos do SharePoint para sincronizar o catálogo do servidor de relatório com itens em bibliotecas de documentos.
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e05dfa8cf6b519468ec631c5b6aa0eb49c040141
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934254"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint"></a>Ativar o recurso de sincronização de arquivo do servidor de relatório no SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

O recurso Sincronização de arquivos do Servidor de Relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utiliza manipuladores de eventos do SharePoint para sincronizar o catálogo do servidor de relatório com itens em bibliotecas de documentos. Esse recurso é benéfico quando os usuários carregam com frequência itens de relatórios publicados diretamente nas bibliotecas de documentos do SharePoint. Se o recurso de Sincronização de arquivo não estiver ativado, o conteúdo ainda será sincronizado, mas não tão frequentemente.

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.
  
 O recurso Sincronização de Arquivos pode ser ativado na Administração de Site do SharePoint depois que você instala o Suplemento [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para produtos do SharePoint.  
  
 Esse recurso pode ser ativado e desativado manualmente por site, mas não no nível de conjunto de sites.  
  
## <a name="prerequisites"></a>Pré-requisitos

 O Suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para o SharePoint deve ser instalado. Se o suplemento não estiver instalado, o recurso de sincronização de arquivos não estará visível na lista de recursos do site.  
  
 Para verificar a instalação, exiba a lista de aplicativos instalados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Painel de Controle **do**Windows. Se o Suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] estiver instalado, siga as instruções deste tópico para ativar o recurso Sincronização de arquivos do servidor de relatório.  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>Para ativar ou desativar o recurso de sincronização de arquivo do Reporting Services em um site
  
1.  Na página principal do site, clique no menu **Ações do Site** e clique em **Configurações do Site**.  
  
2.  Em **Ações de Site** , clique em **Gerenciar Recursos de Site**.  
  
3.  Localize **Sincronização de arquivos do Servidor de Relatório** na lista.  
  
4.  Clique em **Ativar**.  

> [!NOTE]
> Para desativar o recurso Sincronização de arquivos do Servidor de Relatório, é possível usar o mesmo procedimento, mas clique em **Desativar**.

## <a name="see-also"></a>Confira também

 [Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
 [Instalar ou desinstalar o suplemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Instalar ou desinstalar o suplemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
