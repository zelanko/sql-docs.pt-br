---
title: "Ativar o servidor de relatório e recursos de integração do Power View no SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: e97378914a59fab938fc3e4c7926847effcffc94
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>Ativar o servidor de relatório e recursos de integração do Power View no SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Os recursos de coleta de site do Reporting Services são ativados por padrão, depois de instalar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] suplemento para produtos do SharePoint. Em algumas situações, você precisa ativar manualmente os recursos.  

> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.

 Se você instalar o suplemento Reporting Services para produtos do SharePoint 2010 depois da instalação do produto do SharePoint, em seguida, o recurso de integração do servidor de relatório e o recurso de integração do Power View só serão ativados para coleções de sites raiz. Para outras coleções de sites, você precisa ativar manualmente os recursos. Por exemplo, se você tiver um conjunto de sites **http://[my o nome do servidor] /sites/ [nome de coleção do site]** você precisará ativar manualmente os recursos de coleta de site do Reporting Services.  
  
 Quando não há nenhum conjunto de sites raiz, o suplemento Reporting Services registrará uma mensagem semelhante à seguinte.  
  
 "O aplicativo Web SharePoint 80 não tem a coleção de sites raiz"  
  
 A mensagem é encontrada no log de instalação do suplemento, denominado "RS_SP_ #. log" em que # é um número incrementado. O arquivo de log for encontrado na pasta Temp de usuários atual, por exemplo C:\Users\\[nome do usuário] \AppData\Local\Temp.. Para obter mais informações sobre como registrar opções em log com o suplemento, consulte [Instalar ou desinstalar o suplemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  

## <a name="activate-the-report-server-and-power-view-integration-site-collection-features"></a>Ativar os recursos de coleção de sites de integração de servidor de relatório e o Power View
  
1.  Abra seu navegador para o site onde você deseja que os recursos do Reporting Services ativo.  
  
2.  Clique em **Ações do Site**.  
  
3.  Clique em **Configurações de Site**.  
  
4.  Clique em **Recursos do Conjunto de Sites** no Grupo Administração do Conjunto de Sites.  
  
5.  Localize **Recurso de Integração do Servidor de Relatório** ou **Recurso de Integração do Power View** na lista.  
  
6.  Clique em **Ativar**.  
  
 Para desativar os recursos, é possível usar o mesmo procedimento, mas clique em **Desativar** em vez de **Ativar**.  
  
## <a name="activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a>Ativar ou recurso de coleção do site de administração central de desativar o Reporting Services
  
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

