---
title: Compatibilidade com versões de controle do Visualizador de Relatórios
description: O controle do Microsoft Report Viewer é compatível com o SQL Server Reporting Services e o Servidor de Relatórios do Power BI que seguem a política de ciclo de vida de suporte moderna.
author: maggiesMSFT
ms.custom: seo-lt-2019
ms.author: maggies
ms.reviewer: jonhp
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.date: 12/01/2020
ms.openlocfilehash: f6c713d579042425dc863b7d4f942229a091d0c4
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96502690"
---
# <a name="support-for-report-viewer-current-branch-versions"></a>Suporte para versões do branch atual do Visualizador de Relatórios

**_Aplica-se a: Microsoft Report Viewer versões 150.900.148 e posteriores_**

O **controle do Microsoft Report Viewer** é compatível com o SQL Server Reporting Services e o Servidor de Relatórios do Power BI que seguem a [política de ciclo de vida de suporte](https://support.microsoft.com/hub/4095338/microsoft-lifecycle-policy) moderna da Microsoft. Essas informações se aplicam às versões do **ASP.NET** e do **WinForms** distribuídas por meio do [NuGet](https://www.nuget.org/). Todas as versões estão disponíveis por meio do [NuGet](https://www.nuget.org/). Patches, recursos ou outras atualizações são implantados para a versão mais recente. As versões mais recentes devem ser aplicadas para receber alterações. O Visualizador de Relatórios continua a receber **Atualizações de Segurança e Críticas**, com pelo menos um ano de aviso prévio de quaisquer alterações à política de suporte.

Para um histórico de versão do controle do Visualizador de Relatórios, confira os links a seguir:

- [Windows Forms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/)
- [ASP.NET Web Forms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WebForms/)

## <a name="application-server-and-report-server-combinations"></a>Combinações de servidores de relatório e de aplicativo

Alguns recursos do controle do Visualizador de Relatórios dependem dos comportamentos padrão do sistema operacional. Portanto, eles podem exigir a execução da mesma versão tanto para o cliente (o servidor de aplicativo que executa o controle do Visualizador de Relatórios) quanto para o servidor (que executa o Reporting Services). Há suporte para as seguintes combinações de servidor de aplicativo e de relatório:

| Servidor de aplicativos | Servidor de relatórios |
| :----------------- | :------ |
| Windows Server 2012 | Windows Server 2012 |
| Windows Server 2012 | Windows Server 2012 R2 |
| Windows Server 2012 R2 | Windows Server 2012 R2 |
| Windows Server 2012 R2 | Windows Server 2012 |
| Windows Server 2016 e posterior | Windows Server 2016 e posterior |

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o controle do Visualizador de Relatórios, confira [Introdução à integração do Reporting Services usando os controles do Visualizador de Relatórios](integrating-reporting-services-using-reportviewer-controls-get-started.md).
