---
title: Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c6c6c314ec55a01fb6f2884cd6a5baace396efaf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33025823"
---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Os recursos do conjunto de sites do Reporting Services são ativados por padrão após a instalação do Suplemento [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para produtos do SharePoint. Em algumas situações, você precisa ativar os recursos manualmente.  

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

 Se você instalar o suplemento Reporting Services para Produtos do SharePoint 2010 após a instalação do produto do SharePoint, os recursos de integração do Servidor de Relatório e do Power View só serão ativados para conjuntos de sites raiz. Para outros conjuntos de sites, você precisa ativar os recursos manualmente. Por exemplo, se você tiver um conjunto de sites **http://[my server name]/sites/[site collection name]**, precisará ativar os recursos do conjunto de sites do Reporting Services manualmente.  
  
 Quando não houver nenhum conjunto de sites raiz, o suplemento Reporting Services registrará uma mensagem semelhante à mostrada a seguir.  
  
 "O aplicativo Web SharePoint 80 não tem a coleção de sites raiz"  
  
 A mensagem é encontrada no log de instalação do suplemento, chamada “RS_SP_#.log”, em que # é um número de incremento. O arquivo de log é encontrado na pasta Temp de usuários atuais, por exemplo, C:\Users\\[user name]\AppData\Local\Temp. Para obter mais informações sobre como registrar opções em log com o suplemento, consulte [Instalar ou desinstalar o suplemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  

## <a name="activate-the-report-server-and-power-view-integration-site-collection-features"></a>Ativar os recursos de integração de conjunto de sites do Servidor de Relatório e do Power View
  
1.  Abra o navegador no site em que deseja que os recursos do Reporting Services fiquem ativos.  
  
2.  Clique em **Ações do Site**.  
  
3.  Clique em **Configurações de Site**.  
  
4.  Clique em **Recursos do Conjunto de Sites** no Grupo Administração do Conjunto de Sites.  
  
5.  Localize **Recurso de Integração do Servidor de Relatório** ou **Recurso de Integração do Power View** na lista.  
  
6.  Clique em **Ativar**.  
  
 Para desativar os recursos, é possível usar o mesmo procedimento, mas clique em **Desativar** em vez de **Ativar**.  
  
## <a name="activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a>Ativar ou desativar o recurso de conjunto de sites da administração central do Reporting Services
  
1.  Abra seu navegador na Administração Central do SharePoint.  
  
2.  Clique em **Ações do Site**.  
  
3.  Clique em **Configurações de Site**.  
  
4.  Clique em **Recursos do Conjunto de Sites** no Grupo Administração do Conjunto de Sites.  
  
5.  Localize **Recurso da Administração Central do Servidor de Relatório** na lista.  
  
6.  Clique em **Ativar**.  
  
 Para desativar o recurso, é possível usar o mesmo procedimento, mas clique em **Desativar** em vez de **Ativar**.  
  
## <a name="next-steps"></a>Próximas etapas

Depois que o recurso for ativado, será possível continuar com a integração do servidor.

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
