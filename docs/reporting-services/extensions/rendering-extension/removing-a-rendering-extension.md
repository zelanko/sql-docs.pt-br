---
title: Removendo uma extensão de renderização | Microsoft Docs
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0ee3563074e2379061006b72f55dab99f80094cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193457"
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
  
  
