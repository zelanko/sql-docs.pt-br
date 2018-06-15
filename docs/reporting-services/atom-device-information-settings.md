---
title: Configurações de informações de dispositivo ATOM | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fe4a56a4-5552-423c-85c1-895e2e212fee
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5f5c75583542dd7f2bc62b6de5da2fb457a90296
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33014003"
---
# <a name="atom-device-information-settings"></a>Configurações de informações do dispositivo ATOM
  As configurações das informações de dispositivo para a extensão de renderização Atom dão suporte ao envio do nome de um feed Atom e de uma codificação de caracteres a ser usada.  
  
 A tabela a seguir lista as configurações de informações de dispositivo para renderização para um documento de serviço de dados.  
  
|Configuração|Valor|  
|-------------|-----------|  
|**DataFeed**|Se for especificado, renderiza o feed Atom que corresponde ao nome do feed fornecido nessa configuração. Se não, renderiza o documento do serviço Atom para o relatório. O identificador exclusivo gerado automaticamente do feed de dados. Este valor é usado internamente e você não deve alterar isto.|  
|**Codificação**|O nome da IANA (Internet Assigned Numbers Authority) de uma codificação de caracteres com suporte do .NET Framework. O valor padrão é **UTF-8**. Exemplos de outros valores incluem ASCII, UTF-7 e UTF-16.|  
  
## <a name="see-also"></a>Consulte Também  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passando configurações de informações de dispositivos para extensões de renderização](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
