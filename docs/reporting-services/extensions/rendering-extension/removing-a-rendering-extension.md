---
title: "Removendo uma extensão de renderização | Microsoft Docs"
ms.custom: 
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: "38"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0ac5e10f4ea1aa66a4acf38bd0c4b64c3eb8be72
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="removing-a-rendering-extension"></a>Removendo uma extensão de renderização
  Para remover uma extensão de renderização do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], basta remover o elemento **Extension** da extensão de renderização do arquivo rsreportserver.config, localizado em **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<Instance Name>\Reporting Services\ReportServer** folder. Se você criou entradas para um Designer de Relatórios, bem como para um servidor de relatório, remova o elemento **Extension** do [Arquivo de configuração RSReportDesigner](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md) também. Após a remoção das informações de configuração, a extensão de renderização não estará mais disponível para o componente.  
  
## <a name="see-also"></a>Consulte Também  
 [Arquivos de configuração do Reporting Services](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Implementando uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Visão geral das extensões de renderização](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [Implementando a interface IRenderingExtension](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [Considerações sobre segurança para extensões](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [Implantando uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  
