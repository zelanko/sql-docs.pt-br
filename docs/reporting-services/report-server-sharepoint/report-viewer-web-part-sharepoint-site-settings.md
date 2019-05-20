---
title: Configurações do site do SharePoint para a web part do Visualizador de Relatórios – SSRS | Microsoft Docs
ms.date: 11/15/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: jt000
ms.author: jasontre
ms.openlocfilehash: 738908549caa157557a16b1ae05575231a15c734
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65580585"
---
# <a name="sharepoint-site-settings-for-the-report-viewer-web-part---reporting-services"></a>Configurações do site do SharePoint para a web part do Visualizador de Relatórios – Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2016-2019](../../includes/ssrs-appliesto-sharepoint-2016-2019.md)] [!INCLUDE[ssrs-appliesto-not-sharepoint-online](../../includes/ssrs-appliesto-not-sharepoint-online.md)]

A Web Part do Visualizador de Relatórios tem algumas configurações que podem ser definidas. Essas configurações podem ser habilitadas e desabilitadas na página de configurações do site do SharePoint por um administrador de site. Cada site tem suas próprias configurações. Além disso, essas configurações não serão redefinidas após a reinstalação da Web Part do Visualizador de Relatórios.

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
|Coletar dados de uso|Permite que as informações de erro e de uso sejam enviadas à Microsoft para ajudar a melhorar nossos produtos. Para a política de coleta de dados de relatório de erros da Microsoft, consulte a [Política de Privacidade do Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkID=868444).|  
|Habilitar metadados de acessibilidade para relatórios|Define as [informações do dispositivo `AccessibleTablix`](../html-device-information-settings.md) para relatórios renderizados.| 
