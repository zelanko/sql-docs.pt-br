---
title: Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c7f64a54-c555-4d31-bf99-3abe57dc8626
caps.latest.revision: 5
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 45266427e7946e62a758ce994531126324dca39d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37155847"
---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint
  Os recursos da coleção de sites [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] geralmente são ativados por padrão após a instalação do Suplemento [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] para produtos SharePoint. Em algumas situações, você precisará ativar manualmente os recursos.  
  
 Se você instalar o suplemento do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para Produtos SharePoint 2010 depois da instalação do produto SharePoint, o recurso de integração de Servidor de relatório e o recurso de integração do Power View só será ativado para coleções de sites de raiz. Para outras coleções de sites, você precisará ativar manualmente os recursos. Por exemplo, se você tiver um conjunto de sites **http://[my o nome do servidor] /sites/ [nome de coleção de sites]** você precisará ativar manualmente o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] recursos da coleção de sites.  
  
 Quando não há nenhum conjunto de sites raiz, o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] suplemento registrará uma mensagem semelhante à seguinte.  
  
 "O aplicativo Web SharePoint 80 não tem a coleção de sites raiz"  
  
 A mensagem será localizada no log de instalação do suplemento, denominado "RS_SP_#.log", onde # é um número de incremento. O arquivo de log será localizado na pasta Temp de usuários atual, por exemplo C:\Users\\[nome de usuário]\AppData\Local\Temp. Para obter mais informações sobre as opções de registro em log com o suplemento, consulte [instalar ou desinstalar o suplemento Reporting Services para SharePoint &#40;do SharePoint 2010 e SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  
  
 Neste tópico:  
  
-   [Para ativar o Servidor de Relatório e os recursos de coleção de sites do Power View:](#bkmk_features)  
  
-   [Para ativar ou desativar o recurso de coleção de sites da Administração Central do Reporting Services:](#bkmk_centraladmin)  
  
##  <a name="bkmk_features"></a> Para ativar o Servidor de Relatório e os recursos de coleção de sites do Power View:  
  
1.  Abra seu navegador no site em que você deseja que os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] estejam ativos.  
  
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
 [Instalar ou desinstalar o Reporting Services suplemento para SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
