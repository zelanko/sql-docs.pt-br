---
title: Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c7f64a54-c555-4d31-bf99-3abe57dc8626
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e30ae6ea0e7fa314748c4da265650273c0a7d56e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66110033"
---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint
  Os [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] recursos do conjunto de sites geralmente são ativados por padrão depois [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] que você instala o suplemento para produtos do SharePoint. Em algumas situações, você precisará ativar manualmente os recursos.  
  
 Se você instalar o suplemento do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para Produtos SharePoint 2010 depois da instalação do produto SharePoint, o recurso de integração de Servidor de relatório e o recurso de integração do Power View só será ativado para coleções de sites de raiz. Para outras coleções de sites, você precisará ativar manualmente os recursos. Por exemplo se você tiver uma coleção de sites de **http://[nome do meu servidor]/sites/[nome da coleção de sites]** , será necessário ativar manualmente os recursos da coleção de sites do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
 Quando não houver nenhuma coleção de sites raiz, o suplemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] registrará em log uma mensagem semelhante à seguinte.  
  
 "O aplicativo Web SharePoint 80 não tem a coleção de sites raiz"  
  
 A mensagem será encontrada no log de instalação do suplemento, chamado "RS_SP_ #. log", em que # é um número de incremento. O arquivo de log será encontrado na pasta Temp Users atual, por exemplo,\\C:\Users [nome de usuário] \AppData\Local\Temp. Para obter mais informações sobre opções de log com o suplemento, consulte [instalar ou desinstalar o suplemento Reporting Services para sharepoint &#40;sharepoint 2010 e sharepoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  
  
 Neste tópico:  
  
-   [Para ativar o servidor de relatório e Power View os recursos do conjunto de sites de integração:](#bkmk_features)  
  
-   [Para ativar ou desativar Reporting Services recurso de conjunto de sites de administração central:](#bkmk_centraladmin)  
  
##  <a name="bkmk_features"></a>Para ativar o servidor de relatório e Power View os recursos do conjunto de sites de integração:  
  
1.  Abra seu navegador no site em que você deseja que os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] estejam ativos.  
  
2.  Clique em **Ações do Site**.  
  
3.  Clique em **Configurações de Site**.  
  
4.  Clique em **Recursos do Conjunto de Sites** no Grupo Administração do Conjunto de Sites.  
  
5.  Localize **Recurso de Integração do Servidor de Relatório** ou **Recurso de Integração do Power View** na lista.  
  
6.  Clique em **Ativar**.  
  
 Para desativar os recursos, é possível usar o mesmo procedimento, mas clique em **Desativar** em vez de **Ativar**.  
  
##  <a name="bkmk_centraladmin"></a>Para ativar ou desativar Reporting Services recurso de conjunto de sites de administração central:  
  
1.  Abra seu navegador na Administração Central do SharePoint.  
  
2.  Clique em **Ações do Site**.  
  
3.  Clique em **Configurações de Site**.  
  
4.  Clique em **Recursos do Conjunto de Sites** no Grupo Administração do Conjunto de Sites.  
  
5.  Localize **Recurso da Administração Central do Servidor de Relatório** na lista.  
  
6.  Clique em **Ativar**.  
  
 Para desativar o recurso, é possível usar o mesmo procedimento, mas clique em **Desativar** em vez de **Ativar**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois que o recurso for ativado, será possível continuar com a integração do servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar ou desinstalar o suplemento Reporting Services para SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
