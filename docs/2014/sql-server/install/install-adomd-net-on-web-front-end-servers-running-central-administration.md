---
title: Instalar o ADOMD.NET em servidores front-end da Web executando a administração central | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c2372180-e847-4cdb-b267-4befac3faf7e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b77948b3ae5b27d7ecb82c277424057fe39ff7a0
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891035"
---
# <a name="install-adomdnet-on-web-front-end-servers-running-central-administration"></a>Instalar o ADOMD.NET em servidores Web front-end executando a Administração Central
  Se você instalar o PowerPivot para SharePoint em um farm que tenha a topologia de Administração Central, sem Serviços do Excel ou PowerPivot para SharePoint, baixe e instale a biblioteca cliente do Microsoft ADOMD.NET se quiser acesso completo aos relatórios internos no painel de gerenciamento PowerPivot. Alguns relatórios no painel usam ADOMD.NET para acessar dados internos que fornecem dados de relação sobre o processamento de consultas do PowerPivot e a integridade de servidor no farm.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010  
  
 Para o SharePoint 2013, o provedor é incluído no SQL Server feature pack. Para obter informações sobre como baixar o prepowerpivot. msi, consulte [Microsoft SQL Server 2014 Feature Pack](https://www.microsoft.com/download/details.aspx?id=35577)  
  
### <a name="download-and-install-the-client-library"></a>Baixar e instalar a biblioteca de cliente  
  
1.  Na [página SQL Server 2014 Feature Pack](https://go.microsoft.com/fwlink/?LinkID=296473), encontre Microsoft ADOMD.net.  
  
2.  Baixe o Pacote x64 do programa de instalação `SQL_AS_ADOMD.msi`.  
  
3.  Execute o .msi para instalar a biblioteca.  
  
4.  Reinicie o IIS após a conclusão da instalação. Abra um prompt de comando administrativo e digite **iisreset**.  
  
### <a name="verify-installation"></a>Verifique a instalação  
  
1.  Vá para Windows\Assembly.  
  
2.  Clique com o botão direito do mouse em Microsoft. AnalysisServices. AdomdClient e selecione **Propriedades**.  
  
3.  Clique em **Versão**.  
  
4.  Verifique se a versão inclui 12, 0. \<número de Build > e que a descrição é Microsoft. AnalysisService. AdomdClient.  
  
## <a name="see-also"></a>Consulte também  
 [Painel de Gerenciamento PowerPivot e dados de uso](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data)  
  
  
