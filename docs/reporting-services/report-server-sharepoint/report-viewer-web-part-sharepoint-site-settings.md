---
title: "Configurações do site do SharePoint para a Web Part do Visualizador de Relatórios | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: jt000
ms.author: jasontre
ms.workload: Inactive
ms.openlocfilehash: 82efc86ab7f8b688477439816712e85497b1f03f
ms.sourcegitcommit: 4286dddf27dcdf1c8ef3ef134474e72559c2f65c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2017
---
# <a name="sharepoint-site-settings-for-the-report-viewer-web-part"></a>Configurações do site do SharePoint para a Web Part do Visualizador de Relatórios

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

A Web Part do Visualizador de Relatórios tem algumas configurações que podem ser definidas. Essas configurações podem ser habilitadas e desabilitadas na página de configurações do site do SharePoint por um administrador de site. Observe que cada site tem suas próprias configurações. Além disso, essas configurações não serão redefinidas após a reinstalação da Web Part do Visualizador de Relatórios.

## <a name="accessing-the-site-settings-page"></a>Acessando a página de configurações de site

As configurações de site podem ser acessadas por:

1. No site do SharePoint, selecione o ícone de **engrenagem** no canto superior esquerdo e selecione **Configurações de Site**.

    ![Configurações de site no ícone de engrenagem.](media/sharepoint-site-settings.png)

2. Clicando em **Configurações de Web Part do Visualizador de Relatórios** no grupo de configurações do site do **Reporting Services**.

    > [!NOTE]
    > As configurações de site também podem ser alcançadas navegando-se diretamente para `<site>/_layouts/15/ReportViewerWebPart/ReportViewerWebPartSettings.aspx`

## <a name="report-viewer-web-part-settings"></a>Configurações de Web Part do Visualizador de Relatórios

|Configuração|Comentários|  
|-------------|--------------|  
|Coletar dados de uso|Permite que as informações de erro e de uso sejam enviadas à Microsoft para ajudar a melhorar nossos produtos. Para a política de coleta de dados de relatório de erros da Microsoft, consulte a [Política de Privacidade do Microsoft SQL Server](https://go.microsoft.com/fwlink/?linkid=860782&clcid=0x409).|  
|Habilitar metadados de acessibilidade para relatórios|Define as [informações do dispositivo `AccessibleTablix`](../html-device-information-settings.md) para relatórios renderizados.| 
