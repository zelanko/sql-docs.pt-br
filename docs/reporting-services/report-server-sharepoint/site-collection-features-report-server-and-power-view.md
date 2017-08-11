---
title: "Ativar o servidor de relatório e recursos de integração do Power View no SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c7f64a54-c555-4d31-bf99-3abe57dc8626
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: bca4115307f7bf9dab5ffc9d2ab02ababb209d65
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="site-collection-features---report-server-and-power-view"></a>Recursos do conjunto de sites - o servidor de relatório e o Power View
  Os recursos da coleção de sites [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] geralmente são ativados por padrão após a instalação do Suplemento [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para produtos SharePoint. Em algumas situações, você precisará ativar manualmente os recursos.  
  
 Se você instalar o suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para Produtos SharePoint 2010 depois da instalação do produto SharePoint, o recurso de integração de Servidor de relatório e o recurso de integração do Power View só será ativado para coleções de sites de raiz. Para outras coleções de sites, você precisará ativar manualmente os recursos. Por exemplo se você tiver uma coleção de sites de **http://[nome do meu servidor]/sites/[nome da coleção de sites]** , será necessário ativar manualmente os recursos da coleção de sites do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Quando não houver nenhuma coleção de sites raiz, o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] registrará em log uma mensagem semelhante à seguinte.  
  
 "O aplicativo Web SharePoint 80 não tem a coleção de sites raiz"  
  
 A mensagem será localizada no log de instalação do suplemento, denominado "RS_SP_#.log", onde # é um número de incremento. O arquivo de log será localizado na pasta Temp de usuários atual, por exemplo C:\Users\\[nome de usuário]\AppData\Local\Temp. Para obter mais informações sobre como registrar opções em log com o suplemento, consulte [Instalar ou desinstalar o suplemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  
  
 Neste tópico:  
  
-   [Para ativar o Servidor de Relatório e os recursos de coleção de sites do Power View:](#bkmk_features)  
  
-   [Para ativar ou desativar o recurso de coleção de sites da Administração Central do Reporting Services:](#bkmk_centraladmin)  
  
##  <a name="bkmk_features"></a> Para ativar o Servidor de Relatório e os recursos de coleção de sites do Power View:  
  
1.  Abra seu navegador no site em que você deseja que os recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] estejam ativos.  
  
2.  Clique em **Ações do Site**.  
  
3.  Clique em **Configurações de Site**.  
  
4.  Clique em **Recursos do Conjunto de Sites** no Grupo Administração do Conjunto de Sites.  
  
5.  Localize **Recurso de Integração do Servidor de Relatório** ou **Recurso de Integração do Power View** na lista.  
  
6.  Clique em **Ativar**.  
  
 Para desativar os recursos, é possível usar o mesmo procedimento, mas clique em **Desativar** em vez de **Ativar**.  
  
##  <a name="bkmk_centraladmin"></a> Para ativar ou desativar o recurso de coleção de sites da Administração Central do Reporting Services:  
  
1.  Abra seu navegador na Administração Central do SharePoint.  
  
2.  Clique em **Ações do Site**.  
  
3.  Clique em **Configurações de Site**.  
  
4.  Clique em **Recursos do Conjunto de Sites** no Grupo Administração do Conjunto de Sites.  
  
5.  Localize **Recurso da Administração Central do Servidor de Relatório** na lista.  
  
6.  Clique em **Ativar**.  
  
 Para desativar o recurso, é possível usar o mesmo procedimento, mas clique em **Desativar** em vez de **Ativar**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois que o recurso for ativado, será possível continuar com a integração do servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Instalar ou desinstalar o suplemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
