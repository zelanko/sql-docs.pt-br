---
title: "Implementando uma extensão de renderização | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- rendering extensions [Reporting Services]
- custom rendering extensions [Reporting Services]
- transformations [Reporting Services]
- extensions [Reporting Services], rendering
- rendering extensions [Reporting Services], implementing
ms.assetid: 4a5c64f5-2391-4597-ba3f-81d265b23703
caps.latest.revision: "34"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7a6c035dfda213554f79b62594e75f143c17ec03
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="implementing-a-rendering-extension"></a>Implementando uma extensão de renderização
  Uma extensão de renderização é um componente ou um módulo de um servidor de relatório que transforma dados de relatório e informações de layout para um formato específico do dispositivo. O SQL Server Reporting Services inclui seis extensões de renderização: HTML, Excel, Word, CSV ou Texto, XML, Imagem e PDF. Você pode criar extensões de renderização adicionais para gerar relatórios em outros formatos.  
  
> [!NOTE]  
>  Para determinar quais extensões de renderização estão disponíveis, exiba a lista das extensões instaladas no arquivo RSReportServer.config.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral das extensões de renderização](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
 Introduz como escrever uma extensão de renderização personalizada para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Implementar a interface IRenderingExtension](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)  
 Descreve os atributos de uma extensão de renderização.  
  
 [Implantando uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
 Descreve como implantar uma extensão de renderização em um servidor de relatório.  
  
 [Remover uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/removing-a-rendering-extension.md)  
 Descreve como remover uma extensão de renderização de um servidor de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
